<!--
{
"name": "part-one-whats-a-rule-engine-anyway",
"version" : "0.1",
"title" : "Part I: What's a Rules Engine, anyway?",
"description" : "A high-level summary of the function and purpose of a rules engine.",
"homepage" : "https://github.com/outlearn-content/outlearn-modules",
"freshnessDate" : 2015-07-08,
"license" : "CC BY 4.0"
}
-->

<!-- @section -->

# What's covered in this section

* The definition of a Rules Engine
* The benefits and challenges of a Rules Engine
* What this Outlearn path will cover


<!-- @section -->

### The definition of a Rules Engine

Fundamentally, a rules engine is:

> A technological system, used by organizations, that's *purpose-built to process logical operations*, usually in the form of "When [condition], then [action]".

Rather than encompass a bunch of application components, or provide a discrete function in and of itself, rules engines are narrowly focused on performing and organizing the decision-making processes that usually exist within most applications. Thus, instead of replacing other solutions, they are meant to be augmented by existing ones, through the centralization of rules and logic.

The best way to conceptualize this is to perhaps consider how applications are traditionally created. In the vast majority of circumstances, apps are made to be entirely encapsulated, so that any variables or logical decisions that they process are written in the same code that performs other functionality. So, for example, a Java-powered tax calculator may have the following code that determines the marginal tax rate of an individual based on their salary:

```java
double salary = keyboard.nextDouble();

if (salary > 50000) {
  marginalTaxRate == .25;
  }
else if (salary > 30000) {
  marginalTaxRate == .20;
  }
else {
  marginalTaxRate == .15;
  }
```

As simple as this example is, it isn't hard to consider less straightforward logical constructs, and in particular how complex these become if they are interwoven or co-dependant. An application that simultaneously uses only a few of these kinds of rules, but processes thousands of transactions at a time, can quickly be burdened with bugs if a developer hasn't thought through the myriad of possible outcomes from these logical rules at runtime. And, even if a developer creates perfectly bug-free code for this logic, they still have to consider if the rules are written in such a way that, in runtime, they don't utilize more resources than absolutely necessary to find the desired results.

There are other challenges as well. What if we need to change some of these tax rates? What if we want to modify what ranges are covered by what rates? How about adding new tax brackets entirely? In the above example, since all of this logic lives in the application as Java code, we have to have a developer look through the source, find the code, and make changes. We then have to re-test and re-deploy the application. All of this is incredibly time consuming and expensive, even though the change itself is fundamentally quite simple in principle and small in scope.

All of this, and more, comprise the "problem" that rules engines look to solve.

_(Note that, for the purposes of this path, the BRE (Business Rules Engine) we'll be focusing on is Red Hat's BRMS, which is built upon JBoss Drools, Guvnor, and other open source projects. That said, the concepts behind any rules engine are generally the same.)_

<!-- @section -->

### The benefits and challenges of a Rules Engine

It may seem unusual at first to effectively outsource intellignece from the application that's using the logic anyway, but abstracting logic from application code provides a variety of benefits:

* For logic that needs to be changed or updated often, it is usually time-consuming and expensive to perfom such updates when the logic is expressed in application code. Rules, comparatively, are easier to update, and faster to deploy.
* Logic expressed in programming languages like Java tend to be difficult to understand, especially for those who don't code frequently. Business rules, however, have a more legible syntax that is clearer to experienced programmers and BSA's alike. Furthermore, such rules are much easier to understand outside the context of the application that uses it, reducing the risk of programmatic errors.

Of course, rules engines have costs associated with them as well, including:

* Additional cost.
* Increased complexity, both from a technology environment perspective, and an app development perspective.
* Risk of slower applications, particularly when developers don't leverage the rules engine properly, and/or don't adapt the right mindset when composing rules (rule creation is very different from application development).

Ultimately, however, rules engines can be very beneficial for environments that change rules often, desire faster rules deployment, want more understandable/accessible logic, or manage many rules across a variety of systems.

<!-- @section -->

### What this Outlearn path will cover

This path is intended to provide a high level summary of the process for installing and using Red Hat's BRMS (Business Rules Management System) platform, with some particulars that should be helpful for developers and rules authors alike.

<!-- @end -->
