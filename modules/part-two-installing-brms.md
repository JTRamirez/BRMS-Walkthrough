<!--
{
"name": "part-two-installing-brms",
"version" : "0.1",
"title" : "Part II: Installing BRMS",
"description" : "How to install Red Hat's BRMS solution.",
"homepage" : "https://github.com/outlearn-content/outlearn-modules",
"freshnessDate" : 2015-07-08,
"license" : "CC BY 4.0"
}
-->

<!-- @section -->

# What's covered in this section

* Installing Red Hat Linux Enterprise
* Installing Apache's Maven, and Oracle's Java
* Installing Red Hat's EAP and BRMS
* Installing related software and tools


<!-- @section -->

### Installing Red Hat Linux Enterprise

BRMS should be installed on the most recent non-beta version of Red Hat Enterprise Linux (RHEL).

<!-- @section -->

### Installing Apache's Maven, and Oracle's Java

 with up-to-date versions of Java and Maven installed beforehand. 

* For logic that needs to be changed or updated often, it is usually time-consuming and expensive to perfom such updates when the logic is expressed in application code. Rules, comparatively, are easier to update, and are faster to deploy.
* Logic expressed in programming languages like Java tend to be difficult to understand, especially for those who don't code frequently. Business rules, however, have a more legible syntax that is clearer to experienced programmers and BSA's alike.
* Storing logic for multiple applications in a centralized repository makes it easier to access and edit.

Of course, rules engines have costs associated with them as well, including:

* Additional cost.
* Increased complexity, both from a technology environment perspective, and an app development perspective.
* Risk of slower applications, particularly when developers don't leverage the rules engine properly, and/or don't adapt the right mindset when composing rules (rule creation is very different from application development).

Ultimately, however, rules engines can be very beneficial for environments that change rules often, desire faster rules deployment, want more understandable/accessible logic, or manage many rules across a variety of systems.

<!-- @section -->

### Installing Red Hat's EAP and BRMS

BRMS additionally requires Red Hat’s Enterprise Application Platform (EAP), though this can be packaged together with BRMS as a unified installer.

<!-- @section -->

### Installing related software and tools

Once in place, importing and Java development of any kind is handled by the JBoss BRMS Developer Studio (which is a version of Eclipse with EAP and BRMS-related tools installed), though rules authoring itself is intended to be done via BRMS. Red Hat provides an Eclipse plug-in that integrates some EAP and BRMS development tools into the Java IDE, and packages this into a unified solution as their EAP Development Platform (for RHEL). Much of this is documented in the BRMS 6.1 Administration and Configuration guide (A&C) mentioned earlier.

<!-- @end -->
