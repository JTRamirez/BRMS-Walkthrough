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

BRMS should be installed on the most recent non-beta version of Red Hat Enterprise Linux (RHEL). To download the latest version, simply navigate to Red Hat's Software and Download Center on their Customer Portal:

`https://access.redhat.com/downloads`

Look for the "Red Hat Enterprise Linux" product in the list:

![](https://cloud.githubusercontent.com/assets/15032492/10430080/33a36776-70cb-11e5-86a7-fb83f2ae43fa.PNG)

<!-- @section -->

### Installing Apache's Maven, and Oracle's Java

 with up-to-date versions of Java and Maven installed beforehand. 

<!-- @section -->

### Installing Red Hat's EAP and BRMS

BRMS additionally requires Red Hat’s Enterprise Application Platform (EAP), though this can be packaged together with BRMS as a unified installer.

<!-- @section -->

### Installing related software and tools

Once in place, importing and Java development of any kind is handled by the JBoss BRMS Developer Studio (which is a version of Eclipse with EAP and BRMS-related tools installed), though rules authoring itself is intended to be done via BRMS. Red Hat provides an Eclipse plug-in that integrates some EAP and BRMS development tools into the Java IDE, and packages this into a unified solution as their EAP Development Platform (for RHEL). Much of this is documented in the BRMS 6.1 Administration and Configuration guide (A&C) mentioned earlier.

<!-- @end -->
