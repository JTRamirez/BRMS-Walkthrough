<!--
{
"name": "part-seven-advanced-topics",
"version" : "0.1",
"title" : "Part VII: Advanced topics",
"description" : "Items that might be of interest, even if the dive into the weeds a bit.",
"homepage" : "https://github.com/outlearn-content/outlearn-modules",
"freshnessDate" : 2015-07-08,
"license" : "CC BY 4.0"
}
-->

<!-- @section -->

# What's covered in this section

This section is meant to be a catch-all for information and content that isn't mandatory, or otherwise doesn't make sense in any of the previous sections.

* Modifying the UI/UX of the BRMS web interface

<!-- @section -->

Although limited to "aesthetic" rather than structural changes, the interface presented by BRMS is modifiable to a significant extent by virtue of the fact that it relies on bootstrap.css, and makes its HTML and CSS readily available for access and editing in the file structure. 

In fact, Red Hat actually provides some documentation regarding [how to customize particular user-facing interface elements of BPM and BRMS](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_BRMS/6.1
/html-single/Administration_And_Configuration_Guide) in sections 2.2 - 2.2.5 of their Administration and Configuration Guide for BRMS. They specify file paths and provide simple walkthroughs for editing various images, interfaces, etc. (albeit for BPM more broadly, though it’s essentially the same steps for BRMS).

For more sophisticated/deep modifications, most of the CSS that styles the web application is exposed in user-visible style sheets, and these can be edited as well. The interface is powered by the KIE Workbench web application (which incorperates Drools (among other apps/services), which is constructed on bootstrap.CSS (min), with some customizations by Red Hat. Consequently, most of the styles live in CSS documents that a cursory filetype search can bring up (within the business-central.war directory), with the rest existing as inline styles in the html files utilized by the KIE Workbench web application (represented by the org.kie.workbench.KIEWebapp directory, a subfolder or business-central.war).

Most of these changes have a developer navigate to $EAP_HOME/standalone/deployments/business-central.war to reveal all of these assets, and make edits.

Although their division into folders is explained in part by the aforementioned documentation, it is also fairly inconsistent – uncovering the location of CSS files that dictate actual visible styles required using the developer navigator in Firefox to uncover the source. Undoubtedly, Red Hat didn’t create BRMS with UI/UX changes in mind. That said, it isn’t very difficult, and an understanding of the components that make up KIE and BRMS (Drools, Guvnor, etc) help to explain the organization. And, of course, making changes to the CSS was as simple as editing a document.


Particularly when editing styling that’s inline, using a web inspector is necessary to determine where styles for certain components are dictated.

Most elements – images, buttons, text, fonts, links, lists, tables, backgrounds, and menus – have exposed CSS that can be edited, and the great majority of the visible interface is stored in this way, rather than generated at runtime. The primary CSS files (those that seem to be responsible for most of this user-visible styling) include bootstrap.min.css; forms.css; HumanTasks.css; ProcessList.css; and timebox.css. But there are also many styles which exist inline within various HTML documents, utilized by the Java webapp located in the org.kie.workbench.KIEWebapp directory.

It is worth noting that, although things such as size, margin/padding, and even position could be edited via CSS, doing so would not be advisable since the application handles layout in js and/or Java. Furthermore, some elements exist within iframes, or inherit mandatory styling – such as various panes throughout the interface – and these are (for the most part) not readily customized. 

Finally, in the same org.kie.workbench.KIEWebapp directory are the assets to the Drools application (which essentially powers BRMS), and this too reveals all of the assets that are used in the styling of the interface. Buttons and graphics, for example, are stored in either JPG or GIF form (a few of which are animated), and CSS files dictate styling. Modifying these is as simple as using an image editing suite such as Photoshop or GIMP.

<!-- @end -->
