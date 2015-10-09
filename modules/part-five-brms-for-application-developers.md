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

Do this, then that. imports, local repository lives in working memory.

<!-- @section -->

### Migrating existing rules repositories (BRMS 5.x) to BRMS 6.0+

Red Hat provides backwards compatible API's on 6.0 for 5.x. However, these are deprecated from 6.1 and beyond - those require reqrites as much of the underlying technology is changed.

<!-- @section -->

### Basics of integrating new applications

Knowing all this, one can construct a (highly simplified!) step-by-step for implementing a rules engine alongside existing applications, starting with Java apps in Eclipse or BRMS Developer Studio:
1.	In the Java application to be migrated (i.e. have its logic moved to BRMS), import kie and drools libraries in the app (ensuring coverage of any and all logic to be handled by BRMS). For example, this is the “bare minimum” needed in order for an application to utilize very basic rules located in a local repository:
import org.kie.api.KieServices;
import org.kie.api.runtime.KieContainer;
import org.kie.api.KieBase;
import org.kie.api.runtime.KieSession;
import org.kie.api.runtime.StatelessKieSession;

The needed imports for a particular application are specific to what’s being done, but Red Hat provides guidance for what access and functionality each of these actually provides. In addition, the names are fairly transparent, and speak directly to the interfaces defined before.

2.	Within the app, create methods that utilize the above imports, in order to develop values and logical constraints. This is easier said than done, but these need only be made for variables and logic that need to be presented through BRMS. An example:
private static KnowledgeBase readKnowledgeBase() throws Exception {
KnowledgeBuilder kbuilder =
KnowledgeBuilderFactory.newKnowledgeBuilder();
kbuilder.add(ResourceFactory.newClassPathResource("Temp.drl"),
ResourceType.DRL);
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

<!-- @section -->

### APIs & related documentation

Tables and links go here

<!-- @end -->
