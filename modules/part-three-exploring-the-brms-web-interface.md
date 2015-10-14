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

<!-- @section -->

### The Home page

The first page you see upon logging in is the Home page, which is (ironically enough) fairly boring, and provides nearly no functionality, save for some helpful introductory diagrams and other information.

![](https://cloud.githubusercontent.com/assets/15032492/10494562/f6ad0578-7284-11e5-8195-974edcaf88e8.PNG)

The dearth of useful features - and the plain-ness of the BRMS user interface in general - isn't without reason, however. Red Hat uses a generic template as the base UI for a handful of JBoss middleware and other projects, and a side effect of this is that the template has to support very complex solutions, as well as very narrow ones like BRMS.

The good news is that all the basics are covered: On the top left, the navigation bar displays the Home, Authoring and Deployment menus; at the top right, a simple search bar, a contextual help menu, and an account menu round out the options. Furthermore, the layout itself is responsive, and adapts the page layout to screens from smartphones to desktops.

![](https://cloud.githubusercontent.com/assets/15032492/10494745/2312abb2-7286-11e5-860a-f762746e4444.PNG)

<!-- @section -->

### Authoring: The Project Authoring & Administration pages

The "Authoring" menu in the top navigation has two options: Project Authoring, and Administration

![](https://cloud.githubusercontent.com/assets/15032492/10494044/25192dea-7282-11e5-953a-dd9f3528e612.png)

### Project Authoring
The Project Authoring section is where you'll likely spend the great majority of your time, as it's the page where rules, decision tables and the like can be edited. Beyond that, however, Project Authoring also lets you edit the settings for projects, and group/artifact/version IDs for tracking purposes.

![](https://cloud.githubusercontent.com/assets/15032492/10494959/3b683e2e-7287-11e5-963f-a9ccd0beab6f.PNG)

The leftmost column (empty in the above image) acts as a file naviagor and lists files in groups, for the selected project. The primary window in the center provides a place to perform editing of any kinds. And the bottom section provides an easily accessible module where errors can be caught and identified.

At the top, the white subnavigation bar below the main navigation menu provides functionality specific to Authoring:

* __Explore:__ Lists recently opened and recently edited files
* __New Item:__ Allows for a new project, package, rule file, decision table, or other relevant file to be created in the active directory.
* __Tools:__ Provides a way to launch the project editor (which is opened by default when first navigating to the Project Authoring page). Also links to the Data modeler interface.
* __Repositroy:__ Opens the categories editor.

All of this is perhaps best understood when in use, so let's open up a DRL file (which contains rules) and see what happens:

![](https://cloud.githubusercontent.com/assets/15032492/10494049/2974674c-7282-11e5-9b9e-d044997dfe6d.png)

We're provided with a barebones text editor that allows for us to edit the file itself, as well as some file-specific functionality that's presented in the compressed controls at the top of the main window.

![](https://cloud.githubusercontent.com/assets/15032492/10494063/3232d6b6-7282-11e5-821d-75478eb562df.png)

Their functionality is fairly self-explanatory, but to be sure: the Save function commits any changes made to the file; the Delete function removes the file entirely; the Rename function renames the file; the Copy function allows for a duplicate file to be created; and the Validate function performs a check to ensure that proper syntax has been used throughout the file.

If we open a decision table instead of a DRL file, the surrounding elements of the page are the same, but the content in the main window changes significantly:

![](https://cloud.githubusercontent.com/assets/15032492/10494064/34a0ddd0-7282-11e5-8ac8-b1eee8d8d882.png)

Here, we have a simple spreadsheet editor, and a variety of fields and controls. Along the left side, rows are numbered and retain a (default) Description field, with `+` icons that allow for new rows to be added. Along the top row, we see conditional statements and variables, which are nested (the functionality behind this is explained in Part IV). And, in the body of the spreadsheet itself, we see fields that are populated with data - boolians in this case, but data of practically any type can be used as needed.

### Administration

The Administration section is meant to focus on the highest level of BRMS and the logic used within it. A good way to think of this, if we refer to the handy diagram Red Hat uses on the home page...

![](https://cloud.githubusercontent.com/assets/15032492/10495684/14c86e16-728b-11e5-996d-e16ac14ea0a9.png)

... is to understand that, while Packages and Projects are edited and managed in the Project Authoring section, Repositories and Organizations are managed in the Administration section.

![](https://cloud.githubusercontent.com/assets/15032492/10494052/2d58bdcc-7282-11e5-8686-fed6bc2b050b.png)

When opened, you're immediately presented with the Organizational Unit Manager, which allows for OU's to be created, edited, and deleted, and additionally provides a simple means of assigning repositories to particular organizational units.

At the top, the white subnavigation bar below the main navigation menu provides the following:

* __Organizational Units:__ Launches the OU Manager.
* __Repositories:__ Lists all repositories, provides their address, and gives the option to delete any repository.

<!-- @section -->

### Deployment: The Artifact Repository page

![](https://cloud.githubusercontent.com/assets/15032492/10494047/278ff59a-7282-11e5-8916-baaee5874d77.png)

The last section of the BRMS interface is the Artifact Repository, which provides an interface for JAR files (Maven dependencies) to be uploaded.

![](https://cloud.githubusercontent.com/assets/15032492/10496352/6a91f3aa-728e-11e5-86dc-cf49d7647dfc.PNG)

The main window lists the existing files, and provides their filepath and last modified date, as well as the option to download a file, or open any file and inspect its contents:

![](https://cloud.githubusercontent.com/assets/15032492/10496447/de07d9f8-728e-11e5-939f-f791de1ae3de.PNG)

Helpfully, even as a Maven dependancy, a JAR can be uploaded even if it doesn't have any POM information (a mandatory attribute for Maven), and BRMS will provide a simple form that can be filled out to compensate for this (the information is injected into the JAR itself).

<!-- @end -->
