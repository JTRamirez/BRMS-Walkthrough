<!--
{
"name": "part-six-putting-it-all-together",
"version" : "0.1",
"title" : "Part VI: Putting it all together",
"description" : "Wrapping up this path with a summary of the most important concepts, and how they interrelate.",
"homepage" : "https://github.com/outlearn-content/outlearn-modules",
"freshnessDate" : 2015-07-08,
"license" : "CC BY 4.0"
}
-->

<!-- @section -->

# What's covered in this section

* A high-level summary of everything covered so far
* A final quiz
* Concluding remarks


<!-- @section -->

### Summary

Fundamentally, a rules engine is:

> A system that is *purpose-built to perform logic*, usually in the form of "When [condition], then [action]".

Rather than encompassing a bunch of application components, rules engines are narrowly focused on the decision-making processes that exist within most apps. Thus, they are meant work alongside applications by centralizing the storage of rules and logic, and then processing data against those rules as needed.

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

Select all of the following that constitute _benefits_ to implementing a rules engine.

- [X] Centralizing business rules makes such logic easier to administrate and modify.
- [X] The syntax of business rules is easier to understand and work with, compared to application code.
- [X] Updating business rules is significantly easier, faster, and more cost-effective than updating application code.
- [X] Rules engines can speed up logic processing, especially for applications with many rules.

<!-- @end -->

<!-- @multipleChoice -->

Select all of the following that constitute _pitfalls_ to implementing a rules engine.

- [ ] Business rules and decision tables are harder for non-programmers to understand.
- [X] Rules engines have direct and indirect costs.
- [X] A rules engine introduces some complexity to its environment, and to application development for apps that rely on it.
- [ ] Rules engines require significant hardware and network upgrades to support the platform, in order to avoid large slowdowns in application processing.

<!-- @end -->

<!-- @multipleChoice -->

Which of the following lists everything that must be installed before installing Red Hat's BRMS, _in the correct order_?

- [X] RHEL, Java, Maven, JBoss EAP, BRMS
- [ ] RHEL, JBoss EAP, Maven, BRMS, Java
- [ ] RHEL, Maven, Java, JBoss EAP, BRMS
- [ ] Java, RHEL, JBoss EAP, Maven, BRMS

<!-- @end -->

<!-- @multipleChoice -->

[RESERVED FOR INTERFACE NAV]

- [ ] X
- [ ] X
- [X] Y
- [ ] X

<!-- @end -->

<!-- @multipleChoice -->

[RESERVED FOR INTERFACE NAV]

- [ ] X
- [ ] X
- [X] Y
- [ ] X

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

What is Node.js?

- [ ] A package manager for JavaScript packages
- [ ] A front-end framework for heavy-traffic web applications
- [X] A platform for scalable network applications
- [ ] A system that administrates priviliges and access for applications, systems, and users.

Remember that Node.js is more powerful than any individual use that it can be associated with.

<!-- @end -->


<!-- @section -->

### Concluding remarks and ideas to consider

The

<!-- @end -->
