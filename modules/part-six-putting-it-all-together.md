<!--
{
"name": "part-six-putting-it-all-together",
"version" : "0.9",
"title" : "Part VI: Putting it all together",
"description" : "Wrapping up this path with a summary of the most important concepts, and how they interrelate.",
"homepage" : "https://github.com/JTRamirez/BRMS-Walkthrough",
"freshnessDate" : 2015-10-14,
"license" : "CC BY 4.0"
}
-->

<!-- @section -->

# What's covered in this section

* A high-level summary of everything covered so far
* A final quiz


<!-- @section -->

### Summary

Recall the definition we read at the beginning of this path:

> A Rules Engine is technological system, used by organizations, that's purpose-built to process logical operations, usually in the form of "when [condition], then [action]".

At the end of the day, rules engines are meant to handle logic and decision making better than application code. There are certainly added complexities and costs associated with implementing a rules engine into an environment, but for the landscapes that change rules often, or desire to do a better job of administrading swaths of logic, rules engines offer specialization, efficiency, and access.

**For rule authors**, the BRMS web interface provides an accessible platform with which to create rules. Furthermore, DRL files and decision tables rely on clear syntax and can even (in the case of decision tables) be created using traditional spreadsheet software. In either case, however, the logic itself is meant to be presented clearly, easily edited, and quickly deployed.

Finally, **for developers**, Red Hat's documentation and API's provide guidance for integrating their rules engine into existing Java apps, and their Development Studio streamlines this process. Various services and implementations (accessed by apps via imports and APIs) work in concert to allow for applications to maintain local rules caches, and translate logic from Java code to rules files.

<!-- @section -->

### The final quiz

<!-- @multipleChoice -->

Which of the following is the best definition for a _rules engine_?

- [ ] A platform that stores data and performs calculations for applications.
- [X] A system that stores logic and processes logical operations for applications.
- [ ] An application that can stand-in for many different kinds of other applications.
- [ ] A system that administrates priviliges and access for applications, systems, and users.

<!-- @end -->

<!-- @multipleChoice -->

Which of the following _isn't a benefit_ to implementing a rules engine?

- [ ] The syntax of business rules is easier to understand and work with, compared to application code.
- [X] Rules engines greatly simplify the technology environment they are integrated within.
- [ ] Updating business rules is significantly easier, faster, and more cost-effective than updating application code.
- [ ] Rules engines can speed up logic processing, especially for applications with many rules.

<!-- @end -->

<!-- @multipleChoice -->

Which of the following _isn't a pitfall_ to implementing a rules engine?

- [ ] It can take time for developers to train and acclimate to working with rules engines and the API's they rely on.
- [ ] Rules engines have both direct and indirect costs.
- [ ] A rules engine introduces some complexity to its environment, and to application development for apps that rely on it.
- [X] Rules engines require significant hardware and network upgrades to support the platform, in order to avoid large slowdowns in application processing.

<!-- @end -->

<!-- @multipleChoice -->

Which of the following lists everything that must be installed before installing Red Hat's BRMS, _in the correct order_?

- [X] RHEL, Java, Maven, JBoss EAP, BRMS
- [ ] RHEL, JBoss EAP, Maven, BRMS, Java
- [ ] RHEL, Maven, Java, JBoss EAP, BRMS
- [ ] Java, RHEL, JBoss EAP, Maven, BRMS

<!-- @end -->

<!-- @multipleChoice -->

What's the difference between business rules and decision tables?

- [ ] Business rules are stored in spreadsheets; decision tables are stored in documents.
- [ ] Business rules are stored in .DBR files; decision tables are stored in .DRL files.
- [X] A platform for scalable network applications
- [ ] Business rules are authored ; decision tables are authored in spreadsheets

<!-- @end -->

<!-- @multipleChoice -->

Which of the following lists provides all of the elements that can be stored in a DRL file _in the right order_?

- [X] package, imports, globals, functions, queries, rules
- [ ] package, imports, rules
- [ ] imports, globals, functions, queries, rules, package
- [ ] imports, package, globals, functions, rules

<!-- @end -->

<!-- @multipleChoice -->

```drl
rule "Approve if not rejected"
    agenda-group "approval"
        when
            not Rejection() 
            p : Policy(approved == false, policyState:status)
            exists Driver(age > 25)
            Process(status == policyState)
        then
            log("APPROVED: due to no objections."); 
            p.setApproved(true);
end
```

What's the best way to explain when the above rule fires, in layman's terms?

- [ ] If someone is over 25 years old, approve them for a policy.
- [X] If someone hasn't been rejected, and they're over 25 years old, approve them for a policy if they have not been approved yet.
- [ ] Approve anyone who has not been rejected.
- [ ] If someone hasn't been rejected, and they're over 25 years old, and they've already been pre-approved for a policy, then approve them for a policy.

<!-- @end -->

<!-- @multipleChoice -->

As the rules repository for BRMS is stored externally from all local applications, how does an app access and use that logic?

- [ ] A KieBase installed in the application pings the remote repo, fetches rules when they're needed, and processes logic in working memory (of the application).
- [X] A KieScanner service installed in the application fetches rules and creates a rules cache in application memory at runtime, and updates the local cache by checking for updates periodically; a KieServices service lets the application interact with the cache.
- [ ] A KieScanner service installed in the application fetches rules and creates a rules cache in application at runtime, and updates the local cache whenever KieScanner is restarted; a KieSession 
- [ ] A KieServices service provides a unified interface whereby a rules cache is generated at runtime and stored in application memory; any and all rules updates or logic processing is handled by it.

<!-- @end -->
