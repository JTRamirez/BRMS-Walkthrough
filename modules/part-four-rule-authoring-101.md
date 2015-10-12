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

Although the Project Authoring interface enables one to create a variety of files, the two primary file types that tend to contain the great majority of the logic are DRL files, and Decision Tables.

####DRL Files

DRL files are "Drools Rule Language" files (recall that Red Hat BRMS is built upon [Drools](http://drools.org/), among other projects). They are intended to hold all of the discrete rules a particular application may need, and in many respects the writing paradigm may remind a developer of programming in a modern language such as Java - rules group content in curly braces, indents are used to organize content, and so forth.

The file itself has a particular structure, which looks like this:

```drl
package package-name

imports // Can contain things like Java classes and types, that might be used in rules

globals // Generally provide static information for rules

functions // Operations rules can perform when fired

queries // Pulls data for use in rule processing

rules // The rules themselves
```

Outside of declaring the package name, none of these elements is mandatory, and with the exception of rules, adding these elements is done in a simelar fashion to doing the same in Java. Even rules can be omitted, in fact, though the practicality of that is unsurprisingly questionable.

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

Such that, an example of a simple rule that filters auto insurance applicants might look like:

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

Finally, rules themselves can utilize keywords, which are either _hard_ or _soft_. 

The difference (Statements versus inter-related tableture. How they're authored. How they're stored)


####Decision Tables

Decision tables are notably different from DRL's in that they are structured as spreadsheets, rather than as contiguous files. In fact, standard CSV spreadsheets, and even Excel spreadsheets, can be used as decision tables, making them particulalry accessible and flexible to those who are not accostumed to some of the syntax and 

<!-- @section -->

### Business rules

Composed in files, rules are logical statements. Can be interdependant. Algorithms process data against these rules and yield data back to applications (PHREAK is covered in the Advanced topics section)


<!-- @section -->

### Business rules syntax

2.	Create rules and decision tables that utilize the variables presented by the app, via the BRMS web application interface. Rules are programmatic “When [condition], then [action]”, with their own straightforward syntax. The punctuation is forgiving, and many keywords are available in order to achieve more complex behavior, or set rule precedence). Furthermore, this syntax can even be designed via Domain Specific Languages, or DSLs (which the 6.0 Development Guide documents thoroughly in Section 7.5). An example is below:
rule “Push Message” (The name of the rule)
	when 
		m : Message( status == Message.HELLO, myMessage : message )
		(A fact or condition that, when it evaluates as true…)
	then
		System.out.println( myMessage );
		m.setMessage( “Goodbye!” );
		m.setStatus( Message.GOODBYE );
		update( m );
		(…executes and sends along the “result”)
End

rule “Follow Message”
		when
			Message( status == Message.GOODBYE, myMessage : message )
		then
			System.out.println(“My name: “ + myMessage);
end

As an aside, rules themselves are stored in rule files, which are structured as such (note that each of these elements are optional):

package package-name
imports
globals (Generally provide static information)
functions (Operations rules can perform when fired)
queries (Pulling date for use in rule processing)
rules (The rules themselves)



<!-- @section -->

### Decision tables

Of course, rules and rule files aren’t the only way to create and store logic. Decision tables are an alternate method, which Red Hat describes succinctly as such:

Decision tables are a "precise yet compact" (ref. Wikipedia) way of representing conditional logic, and they are well suited to business level rules. Red Hat JBOSS BRMS supports managing rules in a spreadsheet format. Supported formats are Excel (XLS) and CSV; accordingly, a variety of spreadsheet programs (such as Microsoft Excel) can be utilized… Consider decision tables as a course of action if rules exist that can be expressed as rule templates and data: each row of a decision table provides data that is combined with a template to generate a rule. Decision tables are not recommended for rules that do not follow a set of templates or where there are a small number of rules.

In layman’s terms, decision tables are great when rules or logic are highly related and follow the same structure, and especially when they cover ranges (“When the temperature is under 60, then return “Bring a coat”; When the temperature is over 80, then return “Wear a shirt”; etc.). Same as with rules, these are created via the BRMS web application interface.

<!-- @section -->

### Decision tables syntax

These, too, can be edited directly in BRMS, and can alternately be imported and/or edited as Excel or standard CSV spreadsheets:

<!-- @end -->
