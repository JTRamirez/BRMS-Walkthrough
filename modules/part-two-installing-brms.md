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

![](https://cloud.githubusercontent.com/assets/15032492/10430164/a904474c-70cb-11e5-95aa-6df91877632e.PNG)

You'll be able to download a disc image of the operating system, which can then be installed as any other OS would. Just be sure to install RHEL with a GNOME Desktop GUI, which is an option that can be toggled in the "Software Selection" section of the installer:

![](https://cloud.githubusercontent.com/assets/15032492/10430838/80df799a-70cf-11e5-8d25-867b8c3f32e1.PNG)

(You can always uninstall this and run headless later on, but initial installation and configuration of EAP and BRMS is much easier with a GUI.)

<!-- @section -->

### Installing Apache's Maven, and Oracle's Java

Before installing Red Hat's software, up-to-date versions of Java and Maven must be installed beforehand (in that order).

To install Java, navigate to Oracle's download page:

`http://www.java.com/en/download/manual.jsp`

Look for the Linux x64 Installer download, near the bottom of the page, and download it:

![](https://cloud.githubusercontent.com/assets/15032492/10430268/2c4c63e6-70cc-11e5-8121-af4b62abecae.PNG)

Oracle provides instructions on their website for installation, but you'll likely need root access, so issue the `su` command and enter the root password to gain the necessary privileges. 

Have that password handy, by the way, since you'll invoke root from time to time for installs and for running EAP itself.

For Maven, go to Apache's download page:

`https://maven.apache.org/download.cgi`

Any of the downloads in the box will work, but the source has to be built before use, so it's reccomended to just download the binary and unpack it.

![](https://cloud.githubusercontent.com/assets/15032492/10430383/edcf99de-70cc-11e5-9e74-25e88d2fa075.PNG)

Apache provides simple instructions for installing both on their website, and on the README within the downloaded archive.

<!-- @section -->

### Installing Red Hat's EAP and BRMS

We can now finally install the actual rules engine and associated software! BRMS does require Red Hat’s Enterprise Application Platform (EAP), so we'll first install that. Once again, navigate to Red Hat's Software and Download Center, and look for "Red Hat JBoss Enterprise Application Platform" in the JBoss Development and Management section of the page (about half-way down). Select that, and, on the download page itself, click the download link for "Red Hat JBoss Enterprise Application Platform Installer":

![](https://cloud.githubusercontent.com/assets/15032492/10430709/b3577694-70ce-11e5-8416-caaceaad1cab.PNG)

The download page automatically selects the most recent stable version of any software, so you don't need to worry about manually selecting the latest release. However, on the same page, you can use the Product dropdown to select BRMS and download the rules engine, while you're at it:

![](https://cloud.githubusercontent.com/assets/15032492/10430785/1f87be8c-70cf-11e5-97fc-f4e7d3e03ecf.PNG)

Since both of these downloads are Java packages, just use the Terminal to execute them, and follow the steps in the installer. Using `su` to run as root, `cd` to the directory you've downloaded the applications into, and then run:

`java -jar 'APPLICATION_FILE_NAME.jar'`

For EAP, you'll be presented with a simple interface that checks for compatibility, lets you choose the install directory location, and then installs in place. For BRMS, the interface will have you locate the EAP directory, and will install within.

<!-- @section -->

### Installing related software and tools

Finally, once all else is in place, you'll want to install Red Hat's development tools for integrating BRMS into applications. To that end, Red Hat reccomends that Java development be done with their JBoss BRMS Developer Studio (which itself is just a custom version of Eclipse with EAP and BRMS-focused tools incorperated). Alternatively, plugins for Eclipse that provide the same functionality are available in the Eclipse Marketplace. Meanwhile, rules authoring itself is intended to be done via BRMS. 

Much of this is documented in Red Hat's [BRMS 6.1 Administration and Configuration guide (A&C)](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_BRMS/6.1/html-single/Administration_And_Configuration_Guide/), but to download the JBoss BRMS Developer Studio, one simply navigates to the same Software and Download Center mentioned earlier.

Finally, when you're ready to launch EAP and BRMS, ensure that you're root (`su`) and `cd` to the directory you've installed EAP in (e.g. 'EAP-6.4.0'). Then, enter:

`bin/standalone.sh`

to launch the JBoss Bootstrap Environment, with the script automatically starting all the requisite services:

![](https://cloud.githubusercontent.com/assets/15032492/10431155/82bc47f0-70d1-11e5-93c8-15d356c33c1a.PNG)

<!-- @end -->
