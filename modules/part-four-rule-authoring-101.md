<!--
{
"name": "part-four-rule-authoring-101",
"version" : "0.1",
"title" : "Part IV: Rule authoring 101",
"description" : "An introduction to creating business rules, decision tables, and related logical constructs.",
"homepage" : "https://github.com/outlearn-content/outlearn-modules",
"freshnessDate" : 2015-07-08,
"license" : "CC BY 4.0"
}
-->

<!-- @section -->

# What's covered in this section

* Intoduction to rules and decision tables
* Business rules
* Business rules syntax
* Decision tables
* Decision tables syntax


<!-- @section -->

### Intoduction to rules and decision tables

Although the Project Authoring interface enables one to create a variety of files, the two primary file types that tend to contain the great majority of logic are _DRL files_, and _Decision Tables_. Most of the time, DRL files will be the means with which to write and store logic, but Decision Tables can make more sense for particular instances or use cases.

<!-- @section -->

### Business rules (DRL files)

DRL files are "Drools Rule Language" files (recall that Red Hat BRMS is built upon [Drools](http://drools.org/), among other projects). They are intended to hold all of the discrete rules a particular application may need, and in many respects the writing paradigm for DRL files may remind a developer of programming in a modern language such as Java - indents are used to organize content, functions and various kinds of content are declared with similar syntax, and so forth. That said, many of the finiky rules such as trailing semicolons or mandatory curly braces are omitted, and the rules themselves have a fairly rigid structure that is meant to keep them as readable as possible.

![](https://cloud.githubusercontent.com/assets/15032492/10436472/8f620c10-70f4-11e5-9647-605a79e2ad08.png)

<!-- @section -->

### Business rules syntax

Before we get to the rules themselves, however, the DRL file in its entirety has a particular structure, which looks something like this:

```drl
package package-name

imports // Can contain things like Java classes and types, that might be used in rules

globals // Generally provide static information for rules

functions // Operations rules can perform when fired

queries // Pulls data for use in rule processing

rules // The rules themselves
```

Outside of declaring the package name, none of these elements are mandatory, but the order must follow the above sequence. With the exception of rules, however, adding these elements is done in a simelar fashion to doing the same in Java.

```drl
package exampleDRL

import org.brms.helloworld
import org.brms.example

rule "example rule"
...
```

Rules themselves follow a basic structure:

```drl
rule "name"
	<attributes>
	when
		<condition>
	then
		<outcome>
end
```

Such that, an example of a simple rule that filters auto insurance applicants might look like this:

```drl
rule "Approve if not rejected"
	salience -100
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

Rules have a name that is declared immediately; optional attributes which allow for the behaviour of rules to be modified ("salience" in the above example being a value that determines the priority of rules as they enter the queue to be activated); `when` and `then` elements which determine what fires the rule, and what the rule does once fired; and an `end` statement that closes the rule.

Within attributes alone there are a plethora of options, but Red Hat does a good job of documenting these, as well as all the other additional flags and other features [supported by Drools](http://docs.jboss.org/drools/release/6.3.0.Final/drools-docs/html/index.html). Most of the time, however, the above options will suffice.

Finally, Drools supports a very useful feature called "Domain Specific Languages", or DSLs, which allow one to create a particular rule language that then (behind the scenes) is transformed into proper DRL constructs that the rules engine can use. Develiping a DSL can be complicated, but it's a powerful capability that can help make rules more legible, or even serve as a layer of separation between rule authoring and the technical intracacies that a particular application has. DSLs are beyond the scope of this path, but Red Hat [discusses them extensively](http://docs.jboss.org/drools/release/6.3.0.Final/drools-docs/html/ch08.html#d0e11300) in their Drools documentation.

<!-- @section -->

### Decision tables

Decision tables are notably different from DRLs in that they are structured as spreadsheets, rather than as contiguous files. In fact, standard CSV spreadsheets, and even Excel spreadsheets, can be used as decision tables, making them particulalry accessible and flexible to those who are not accostumed to some of the syntax used in DRLs.

![](https://cloud.githubusercontent.com/assets/15032492/10436458/779a4250-70f4-11e5-80cc-a5c4bda2f35b.png)

The tables themselves are composed of columns and rows, with rows having "Description" labes (which are optional), and columns holding conditinal statements. These statements can be layered or nested, and in many respects they are tantamount to the `when` portion of rules in DRL files.

Consequently, as you might expect the cells that make up these rows and columns represent the `then` portion of rules. Thus, if data fits the critera for a given column, then the appropriate row entry is found, and that value is returned. In the above image, the checkboxes represent bool values, but values of any type can be put into these cells.

<!-- @section -->

### Decision tables syntax

Red Hat describes Decision Tables succinctly as such:

> Decision tables are a "precise yet compact" (ref. Wikipedia) way of representing conditional logic, and they are well suited to business level rules. Red Hat JBOSS BRMS supports managing rules in a spreadsheet format. Supported formats are Excel (XLS) and CSV; accordingly, a variety of spreadsheet programs (such as Microsoft Excel) can be utilized… Consider decision tables as a course of action if rules exist that can be expressed as rule templates and data: each row of a decision table provides data that is combined with a template to generate a rule. Decision tables are not recommended for rules that do not follow a set of templates or where there are a small number of rules.

In layman’s terms, decision tables are great when rules or logic are highly related and follow the same structure, and especially when they cover ranges (“When the temperature is under 60, then return “Bring a coat”; When the temperature is over 80, then return “Wear a shirt”; etc.). And, while as with rules, they can be created via the BRMS web application interface, standard spreadsheet apps can also be used.

<!-- @end -->
