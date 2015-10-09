# Documentation

This path was compiled based on the information available on a wide variety of sources, and thankfully most of theser are freely available online. That said, and somewhat frustratingly, online documentation for much of BRMS and its associated contents (Guvnor, Maven, KIE Workbench, etc.) and APIs (KIE, REST) are either dispersed across many channels, or remain hard to come by altogether – so this resource page will hopefully reduce any necessary hunting should you need to learn anything beyond the scope of this path.

The below links encompass documentation, presentations, videos, and related media that should prove to be helpful in learning more about BRMS, and understanding the process in which it is installed and deployed. This is particularly true for rule authoring (understanding syntax and scope) and app development (APIs, methods, etc.), and I’ve thus organized the links toward these functions.

## Resources for installation:

### Demos:

Part One of Red Hat’s BRMS Cool Store demo walks through a basic installation of BRMS on top of EAP & RHEL. http://www.jboss.org/video/vimeo/65222228/

### Workshops:

Section One of Red Hat’s online workshop provides an online slide deck, as well as instructions for installing BRMS. http://www.schabell.org/2014/03/redhat-jboss-brms-online-workshop-coolstore-intro-lab1-2.html

## Resources for development:

### Demos:

The example projects from Red Hat’s JBoss BRMS Starter Kit – notably, the “Weight Watchers Realtime Decision Server” and “Loan Realtime Decision Server” – are perhaps the most nformative with respect to illustrating what app integration looks like, and how (and what kinds of) logic should be constructed within BRMS. For each of the example projects, functional dummy apps and rules are already configured, and their logic authored, via BRMS. Note that it is highly recommended to use these with a fresh installation of RHEL on a virtual machine, since they necessitate many installations: http://www.schabell.org/p/jboss-brms-starter-kit.html

Ruling with Drools RE. An excellent walkthrough (with full example) of implementing a rules engine in a Java app. The example uses a local rules repository, rather than a remote/centralized one, but the guide is informative nevertheless https://pkghosh.wordpress.com/2010/11/20/ruling-with-drools-rule-engine/ 

## Resources for rule creation:

Parts Two & Three of Red Hat’s BRMS Cool Store demos – illustrates rule creation, guided decision tables, and navigating BRMS’s interface.
•	Part 2: http://www.jboss.org/video/vimeo/65224122/
•	Part 3: http://www.jboss.org/video/vimeo/65226780/
Sections 2-10 of Red Hat’s online workshop – offers  a walkthrough of BRMS installation, rule authoring, creating tables, and running through test scenarios via the Cool Store demo.
•	http://www.schabell.org/2014/03/redhat-jboss-brms-online-workshop-coolstore-intro-lab1-2.html

## Additional content:
Red Hat’s Cool Store Demo is available as a git repo at the following address, with instructions for installation (ensure that Java and Maven are installed beforehand, and include the Red Hat software when installing as instructed by the included documentation):
•	https://github.com/jbossdemocentral/brms-coolstore-demo/tree/v2.0

For some reason, the HTML/hosted version of Red Hat’s JBoss BRMS 6.0 Development Guide deviates from the downloadable PDF version noticeably, and contains both more content, and more sections. I highly suggest reading through it (with a focus on Sections 2-3 for those unfamiliar with Rules Engines; Sections 4-5 for key development information; and Sections 6 and 8 for rule authoring):
•	https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_BRMS/6.0/html-single/Development_Guide/ 
The documentation for JBoss Drools is much more complete, and resources for Drools much more prevalent, than the equivalent online resources for Red Hat’s BRMS solution. However, BRMS is essentially a repackaged version of Drools, and thus much of the documentation for the latter applies to the former. Particularly for rule authoring, syntax, API information, and development guidance, the following resources should be of use:
•	Drools 6.3.0 final documentation (always look for up-to-date documentation on the drools.org website): http://docs.jboss.org/drools/release/6.3.0.Final/drools-docs/html_single/index.html
•	Drools helloworld-brms example project: http://www.jboss.org/quickstarts/brms/helloworld-brms/
•	Drools 6.0 Red Hat Summit presentation deck (includes example projects & git repos, video tutorials, and in-depth discussion of rule authoring, decision tables & scorecards): http://www.slideshare.net/MarkProctor/drools-60-red-hat-summit-34589970#

