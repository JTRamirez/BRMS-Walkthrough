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

<br /><br />

# The definition of a Rules Engine

Fundamentally, a rules engine is:

> A technological system, used by organizations, that's *purpose-built to process logical operations*, usually in the form of "when [condition], then [action]".

Rather than encompass a bunch of application components, or provide a discrete function in and of itself, rules engines are narrowly focused on performing and organizing the decision-making processes that usually exist within the code of most applications. Thus, instead of replacing other solutions, they are meant to be augmented by existing ones, through the centralization of rules and logic.

The best way to conceptualize this is to consider how applications are traditionally created. In the vast majority of circumstances, apps are made to be entirely encapsulated, so that any variables or logical decisions that they process are written in the same code that performs all other functionality. So, for example, a Java-powered tax calculator may have the following code (a function call) that determines the marginal tax rate of an individual based on their income:

```java
findIndividualMarginalTaxRate(double income) {
  if (income > 90750) {
    marginalRate == .28;
    }
  else if (income > 37450) {
    marginalRate == .25;
    }
  else if (income > 9225) {
    marginalRate == .15;
    }
  else {
    marginalRate == .1;
    }
  return marginalRate;
}
```

As simple as this example is, it isn't hard to consider less straightforward logical constructs, and in particular how complex these become if they are interwoven or co-dependant. Imagine if we also function calls for determining which tax rates apply to various individuals, and had to roll these up into a function that would select the correct tax schedule to use in calculation:

```java
marrigeStatus(bool isMarried) {
  if (married == 1) {
    return 1;
    }
  return 0;
}

jointRetun(bool relationshipStatus, bool isJoint) {
  if (marriageStatus(relationshipStatus) == 1) {
    if (bool isJoint == 1) {
     return 1; 
    }
  }
  return 0;
}

headOfHousehold(bool isHeadOfHousehold) {
  if (isHeadOfHousehold == 1) {
    return 1;
  }
  return 0;
}
```

The resultant wrapped-up function (utilizing the included class to return necessary values) might look like this:

```java
final class taxProfile {
  private final double marginalRate;
  private final int standardDeduction;
  
  public myTaxProfile(double marginalRate, int standardDeduction) {
    this.marginalRate = marginalRate;
    this.standardDeduction = standardDeduction;
  }

  public double getMarginalRate() {
    return marginalRate;
  }

  public int getStandardDeduction() {
    return standardDeduction;
  }
}

...

selectTaxRateSchedule(bool isMarried, bool isJoint, bool isHeadOfHouse, bool isTrustOrEstate, double income) {
  if (marrigeStatus(isMarried) == 1) {
    if jointReturn(isJoint) == 1) {
      return new myTaxProfile(findJointMarginalTaxRate(income), 12600);
    }
    else {
      return new myTaxProfile(findIndividualMarriedMarginalTaxRate(income), 6300);
    }
  }
  else if (headOfHousehold(isHeadOfHouse) == 1) {
    return new myTaxProfile(findHeadOfHouseholdMarginalTaxRate(income), 9250);
  }
  else if (trustAndEstate(isTrustOrEstate) == 1) {
    return new myTaxProfile(findTrustAndEstateMarginalTaxRate(income), 0);
  }
  else {
    return new myTaxProfile(findIndividualMarginalTaxRate(income), 6300);
  }
  throw new IncorrectDataException();
}
```

And this is all just to find the right schedule! We haven't even begun to consider many deductions, or all of the other rules and conditions that apply before we can perform calculation. And this is with fairly repetitive logic that's using very obvious names for variables and functions.

Hopefully, this helps to illustrate how combining simple rules and churning thousands of transactions through them can quickly be burdensome, and prone to bugs if a developer hasn't thought through the myriad of possible outcomes from these logical rules at runtime. And, even if a developer creates perfectly bug-free code for this logic, they still have to consider if the rules are written in such a way that, in runtime, they don't utilize more resources than absolutely necessary to find the desired results. In the above example, does it make sense to deduce individual tax filers last, instead of heads of household? Is it prudent to check marital status as a precursor to checking whether or not someone is filing jointly? How would we know?

There are other challenges as well. What if we need to change some of these tax rates? What if we want to modify what ranges are covered by what rates? How about adding new tax brackets entirely? In the above example, since all of this logic lives in the application as Java code, we have to have a developer look through the source, find the code, and make changes. We then have to re-test and re-deploy the application. All of this is incredibly time consuming and expensive, even though the change itself is fundamentally quite simple in principle and small in scope.

All of this, and more, comprise the "problem" that rules engines look to solve.

_(Note that, for the purposes of this path, the BRE (Business Rules Engine) we'll be focusing on is Red Hat's BRMS, which is built upon JBoss Drools, Guvnor, and other open source projects. That said, the concepts behind any rules engine are generally the same.)_

<!-- @section -->

### The benefits and challenges of a Rules Engine

It may seem unusual at first to effectively outsource intellignece from the application that's using the logic anyway, but abstracting logic from application code provides a variety of benefits:

* For logic that needs to be changed or updated often, it is usually time-consuming and expensive to perfom such updates when the logic is expressed in application code. A developer has to find the code that contains the logic, and then make changes. Those changes have to be tested for QA purposes. And then the updated application has to be deployed. Rules, comparatively, are easier to update, and faster to deploy - even a non-programmer can concievably use the BRMS interface to update rules in real time, and then deploy them to live applications without interruption, and without the risk of introducting bugs in the application code.
* Logic expressed in programming languages like Java tend to be difficult to understand, especially for those who don't code frequently. Even a developer can have trouble understanding the context of a function within an application if they didn't write it themselves. Business rules, however, have a more legible syntax that is clearer to experienced programmers and BSA's alike. Furthermore, such rules are much easier to understand outside the context of the application that uses it, reducing the risk of programmatic errors.
* As you might expect, administrating rules, and building similar logic across multiple systems, is much easier when business rules and logic are centralized.
* When utilized properly, rules engines can sometimes offer performance benefits to applications by processing logic faster than if the app did it alone. This is particularly true of applications that process data through logic very often - BRE's rely on sophistocated algorithms that deduce the most efficient way to process business rules, whereas most applications that encapsulate logic rely on simpler or clearer code at the expense of efficiency.

Of course, rules engines have costs associated with them as well, including:

* Additional costs, both direct (purchasing and maintaining the rules engine and associated hardware/platforms) and indirect (the development and training cost to transition logic into the engine, and train employess how to utilize it).
* Increased complexity, both from a technology environment perspective, and an application development perspective.
* A small risk of slowing down applications, particularly when developers don't leverage the rules engine properly, and/or don't adapt the right mindset when composing rules (_rule creation is very different from application development!_).

Ultimately, however, rules engines can be very beneficial for environments that change rules often, desire faster rules deployment, want more understandable/accessible logic, or manage many rules across a variety of systems.

<!-- @section -->

### What this Outlearn path will cover

This path is intended to provide a high level summary of the process for installing and using Red Hat's BRMS (Business Rules Management System) platform, with some particulars that should be helpful for developers and rules authors alike.

<!-- @end -->
