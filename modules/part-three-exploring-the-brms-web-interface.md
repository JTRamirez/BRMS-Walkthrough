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



![3](https://cloud.githubusercontent.com/assets/15032492/10494044/25192dea-7282-11e5-953a-dd9f3528e612.png)

![4](https://cloud.githubusercontent.com/assets/15032492/10494047/278ff59a-7282-11e5-8916-baaee5874d77.png)

![5](https://cloud.githubusercontent.com/assets/15032492/10494049/2974674c-7282-11e5-9b9e-d044997dfe6d.png)

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

This path is intended to provide a high level summary of the process for installing and using Red Hat's BRMS (Business Rules Management System) platform, with some particulars that should be helpful for developers and rules authors alike. That said, much of the high-level information reflects how rules engines in general tend to work, and aren't specific to Red Hat's solution(s).

<!-- @end -->
