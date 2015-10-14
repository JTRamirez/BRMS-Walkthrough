<!--
{
"name": "part-three-exploring-the-brms-web-interface",
"version" : "0.1",
"title" : "Part III: Exploring the BRMS web interface",
"description" : "Navigating the pages of Red Hat's online BRMS platform.",
"homepage" : "https://github.com/JTRamirez/BRMS-Walkthrough",
"freshnessDate" : 2015-10-14,
"license" : "CC BY 4.0"
}
-->

<!-- @section -->

# What's covered in this section

* Logging in
* The Home page
* Authoring: The Project Authoring & Administration pages
* Deployment: The Artifact Repository page

<!-- @section -->

# Logging in

Once you've launched the JBoss Bootstrap Environment, the webapp service will be running, and you can access the web interface. To do this locally, simply open up a web browser (Firefox is reccomended and pre-installs with RHEL) and navigate to:

`http://localhost:8080/business-central`

You'll land at the login page, where you can use the account you created when installing BRMS to log in for the first time.

![](https://cloud.githubusercontent.com/assets/15032492/10494467/823bdf02-7284-11e5-9da9-9491b71bb3f9.PNG)

![4](https://cloud.githubusercontent.com/assets/15032492/10494047/278ff59a-7282-11e5-8916-baaee5874d77.png)

![6](https://cloud.githubusercontent.com/assets/15032492/10494052/2d58bdcc-7282-11e5-8686-fed6bc2b050b.png)

![9](https://cloud.githubusercontent.com/assets/15032492/10494063/3232d6b6-7282-11e5-821d-75478eb562df.png)

![10](https://cloud.githubusercontent.com/assets/15032492/10494064/34a0ddd0-7282-11e5-8ac8-b1eee8d8d882.png)

<!-- @section -->

### The Home page

The first page you see upon logging in is the Home page, which is (ironically enough) fairly boring, and provides nearly no functionality, save for some helpful introductory diagrams and other information.

![](https://cloud.githubusercontent.com/assets/15032492/10494562/f6ad0578-7284-11e5-8195-974edcaf88e8.PNG)

The dearth of useful features - and the plain-ness of the BRMS user interface in general - isn't without reason, however. Red Hat uses a generic template as the base UI for a handful of JBoss middleware and other projects, and a side effect of this is that the template has to support very complex solutions, as well as very narrow ones like BRMS.

The good news is that all the basics are covered: On the top left, the navigation bar displays the Home, Authoring and Deployment menus; at the top right, a simple search bar, "What's New" release notes module, and an account menu round out the options. Furthermore, the layout itself is responsive, and adapts the page layout to screens from smartphones to desktops.

![](https://cloud.githubusercontent.com/assets/15032492/10494745/2312abb2-7286-11e5-860a-f762746e4444.PNG)

<!-- @section -->

### Authoring: The Project Authoring & Administration pages

The "Authoring" menu in the top navigation has two options: Project Authoring, and Administration

![](https://cloud.githubusercontent.com/assets/15032492/10494044/25192dea-7282-11e5-953a-dd9f3528e612.png)

The Project Authoring section is where you'll likely spend the great majority of your time, as it's the page where rules, decision tables and the like can be edited. Beyond that, however, Project Authoring also lets you edit the settings for projects, and group/artifact/version IDs for tracking purposes.

![](https://cloud.githubusercontent.com/assets/15032492/10494959/3b683e2e-7287-11e5-963f-a9ccd0beab6f.PNG)

The leftmost column (empty in the above image) acts as a file naviagor and lists files in groups, for the selected project. The primary window in the center provides a place to perform editing of any kinds. And the bottom section provides an easily accessible module where errors can be caught and identified.

At the top, the white subnavigation bar below the main navigation menu provides functionality specific to Authoring:

* Explore: Lists recently opened and recently edited files
* New Item: Allows for a new project, package, rule file, decision table, or other relevant file to be created in the active directory.
* Tools: Provides a way to launch the project editor (which is opened by default when first navigating to the Project Authoring page). Also links to the Data modeler interface.
* Repositroy: Opens the categories editor.

All of this is perhaps best understood when in use, so let's open up a DRL file (which contains rules) and see what happens:

![](https://cloud.githubusercontent.com/assets/15032492/10494049/2974674c-7282-11e5-9b9e-d044997dfe6d.png)


<!-- @end -->
