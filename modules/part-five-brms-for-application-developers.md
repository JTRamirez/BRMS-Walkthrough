<!--
{
"name": "part-five-brms-for-application-developers",
"version" : "0.1",
"title" : "Part V: BRMS for application developers",
"description" : "A summary of Red Hat's APIs, and explainers for how an application can integrate with BRMS.",
"homepage" : "https://github.com/outlearn-content/outlearn-modules",
"freshnessDate" : 2015-07-08,
"license" : "CC BY 4.0"
}
-->

<!-- @section -->

# What's covered in this section

* Overview of integrating BRMS with Java applications
* Migrating existing rules repositories (BRMS 5.x) to BRMS 6.0+
* Basic sequence of integrating new applications
* APIs & related documentation


<!-- @section -->

### Overview of integrating BRMS with Java applications

BRMS relies on APIs provided by its individual components - Drools, KIE Workbench, and so forth - to integrate with Java applications. However, it's important to understand how this integration of a remote repository looks at a higher level, encompassing systems, applications and services:

![](https://cloud.githubusercontent.com/assets/15032492/10437076/baedb6b4-70f8-11e5-8f9d-96945a79c536.jpg)

The repository itself exists as a Maven build that contains a POM file (standard for all Maven builds), a kmodule which acts as a deployable unit that contains all the BRMS repository's content for all applications; KieBase(s) that contain rules files for particular applications; and the various DRLs, Tables and associated files that constitute all business rules and logic. 

BRMS/EAP edits these contents via the KIE Workbench web application, and both of these (the instance and the repo) usually co-exist running atop RHEL.

For each application, a service is implemented that does the work of fetching business rules and logic at runtime, and this content is "stored" in working application memory. The same service also polls the kmodule in the remote repositiory at regulated intervals, downloading and refreshing the local rules cache if any changes are detected. Finally, as logic needs to be processed, the application sends inputs to a seperate service, which processes the data against the rules, and feeds the results back into the application.

Let's take a closer look at each of these individual components:

###At the Repository:
<br />
* **KieModule (kmodule):** Fundamentally this represents a deployable unit (a JAR or folder) that contains everything below. As previously explained, the descriptor file it is defined by (the kmodule.xml file) allocates resources to knowledge bases, and configures those bases and sessions. The KieModule requires a pom file (standard for Maven) which handles build order. It coexists with the BRMS app, on top of EAP, in a RHEL instance.
* **KieContainer (kContainer):** Contained within the KieModule. Allows for the lookup of named KieBases and KieSessions (see below). This is essentially a reference for KieServices and KieScanner, which are processes that execute on the application side.
* **KieBase (kbase):** The repository for all of an application’s knowledge definitions – rules, processes, functions, and type models. Note that the KieBase itself doesn’t ever contain data, but rather has sessions created from it with which data is inserted into and processed. Since it stores all logic, it is also fairly resource-heavy (hence deferring rule processing to sessions, which are lightweight and ephemeral).

###At the Application:
<br />
* **KieServices (kservice):** The interface with which an application sends data to a KieSession (which lives on the repository side), and retrieves results. Oversimplifying a bit, this is essentially a group of imports, and some function calls, that allow for the application to interact. This is where applications (primarily) interact with the repository!
* **KieScanner (kscanner):** A service that continuously monitors a Maven repository (remote or local), in order to detect if a new KieModule has been installed (so, when any changes have been committed to the repo). The polling interval can be declared by the developer in-application, and/or changes can be checked for on demand. Whenever a change is detected, the updated module is automatically downloaded, and an incremental build is triggered. This ensures that all new KieSessions use the updated rules (though this likely does not force live sessions to refresh – that would have to be done manually or programmatically).
* **KieSession (ksession):** The process that receives and executes on runtime data in working memory. A KieSession is created when KieServices fetches logic from KieBase (on the repository side) and creates a local rules repository in application working memory – and this local repo is the logic that the application actually works with during execution.  Compared to KieBase, KieSessions are designed to be ephemeral (started and stopped at will) and much less resource intensive, and consequently rule processing is performed through them. This is where the “magic” happens and rules/logic are utilized by applications.



The applications that use the rules only access them indirectly via the KieScanner service, which runs as a part of each application that leverages rules. When the application is first run, KieScanner pulls the pertinent rules stored in the KieBase and generates a local KieSession rules cache that sits in working application memory, ready to be used by the application's KieServices service. Whenever logic needs to be processed, KieServices becomes live, and pushes the necessary data to the KieSession, and the rules are fired accordingly. Any output is sent back to the application, where it can be used. As it is meant to be ephemeral, KieServices is then ended if and when it no longer has queued data.

Meanwhile, throughout the life of the application, KieScanner pings the kmodule indefinintely, seeking out any rule changes or updates that have been saved to KieBase. Whenever this is the case, KieScanner re-downloads the logic, and refreshes the KieSession rules cache accordingly. From that point forward, any new instances of KieServices utilize the new rules.

At the application level, the services (KieScanner, KieServices, and KieSession) that "live" on or with the application itself are obvious, and these are introduced via imports to the Java code. Interactions between the application and these services are handled by APIs that Red Hat documents both in their [Administration and Configuration Guide for BRMS](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_BRMS/6.0/pdf/Administration_And_Configuration_Guide/Red_Hat_JBoss_BRMS-6.0-Administration_And_Configuration_Guide-en-US.pdf), and in their [6.3.0 Final release of JBoss Drool's documentation](http://docs.jboss.org/drools/release/6.3.0.Final/drools-docs/html/index.html).

<!-- @section -->

### Migrating existing rules repositories (BRMS 5.x) to BRMS 6.0+

Red Hat provides backwards compatible APIs on 6.0 for BRMS versions 5.x. However, these are deprecated from 6.1 and beyond - those require reqrites as much of the underlying technology is changed.

<!-- @section -->

### Basics of integrating new applications

Knowing all this, one can construct a (highly simplified!) step-by-step for implementing a rules engine alongside existing applications, starting with Java apps in Eclipse or BRMS Developer Studio:

1. In the Java application to be migrated (i.e. have its logic moved to BRMS), import kie and drools libraries in the app (ensuring coverage of any and all logic to be handled by BRMS). For example, this is the “bare minimum” needed in order for an application to utilize very basic rules located in a local repository:

```java
import org.kie.api.KieServices;
import org.kie.api.runtime.KieContainer;
import org.kie.api.KieBase;
import org.kie.api.runtime.KieSession;
import org.kie.api.runtime.StatelessKieSession;
```

The needed imports for a particular application are specific to what’s being done, but Red Hat provides guidance for what access and functionality each of these actually provides. In addition, the names are fairly transparent, and speak directly to the interfaces defined before.

2. Within the app, create methods that utilize the above imports, in order to develop values and logical constraints. This is easier said than done, but these need only be made for variables and logic that need to be presented through BRMS. An example:

```java
private static KnowledgeBase readKnowledgeBase() throws Exception {
  KnowledgeBuilder kbuilder = KnowledgeBuilderFactory.newKnowledgeBuilder();
  kbuilder.add(ResourceFactory.newClassPathResource("Temp.drl"), ResourceType.DRL);
  KnowledgeBuilderErrors errors = kbuilder.getErrors();
  if (errors.size() > 0) {
    for (KnowledgeBuilderError error: errors) {
      System.err.println(error);
    }
    throw new IllegalArgumentException("Could not parse knowledge.");
  }
  KnowledgeBase kbase = KnowledgeBaseFactory.newKnowledgeBase();
  kbase.addKnowledgePackages(kbuilder.getKnowledgePackages());
  return kbase;
}
```

<!-- @section -->

### APIs & related documentation

Tables and links go here.

<!-- @end -->
