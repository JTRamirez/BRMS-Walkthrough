<!--
{
"name": "part-one-whats-a-rule-engine-anyway",
"version" : "0.9",
"title" : "Part I: What's a Rules Engine, anyway?",
"description" : "A high-level summary of the function and purpose of a rules engine.",
"homepage" : "https://github.com/JTRamirez/BRMS-Walkthrough",
"freshnessDate" : 2015-10-14,
"license" : "CC BY 4.0"
}
-->

<!-- @section -->

# What's covered in this section

* The definition of a Rules Engine
* The benefits and challenges of using a Rules Engine
* What this Outlearn path will cover

<br />

# The definition of a Rules Engine

Fundamentally, a rules engine is:

> A technological system, used by organizations, that's *purpose-built to process logical operations*, usually in the form of "when [condition], then [action]".

Rather than encompass a bunch of application components, or provide a discrete function in and of itself, rules engines are narrowly focused on performing and organizing the decision-making processes that usually exist within the code of most applications. Thus, instead of replacing other solutions, they are meant to be augmented by existing ones, through the centralization of rules and logic.

The best way to conceptualize this is to consider how applications are traditionally created. In the vast majority of circumstances, apps are made to be entirely encapsulated, so that any variables or logical decisions that they process are written in the same code that performs other functionality. So, for example, a Java-powered tax calculator may have the following code (a function call) that determines the marginal tax rate of an individual based on their income:

```java
double findIndividualMarginalTaxRate(double income) {
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
In this case, chained `if` statements get the job done, but the function as a whole can be considered a group of logical choices made by the program - "when income is above 90750, set the marginal rate to .28; when income is above 37450 and below 90750, set the marginal rate to .25...", and so forth.

As simple as the above example may be, however, it isn't hard to consider less straightforward logical constructs, and in particular how complex these become if they are interwoven or co-dependant. Imagine if we also had functions for determining which tax rates apply to various individuals, and then had to roll those up into a unified function that would select the correct tax schedule to use in subsequent calculation. Some of those might include:

```java

String[][] deductionLookup(String[][] claimedDeductions) {
	for(String s: deductionArray[][]) {
		for (int i = 0; i < deductionArray.length; i++) {
		  for (int k = 0; k < claimedDeductions.length; k++) {
		    if (deductionArray[i][0] = claimedDeductions[k][0]) {
		      claimedDeductions[k][1] = Integer.parseInt(deductionArray[i][1]);
		    }
		  }
		}
		return claimedDeductions[][];
	}
  throw new IncorrectDataException();
}

boolean marrigeStatus(boolean isMarried) {
  if (married == true) {
    return true;
    }
  return false;
}

boolean jointRetun(boolean relationshipStatus, boolean isJoint) {
  if (marriageStatus(relationshipStatus) == true) {
    if (bool isJoint == true) {
     return true; 
    }
  }
  return 0;
}

boolean headOfHousehold(bool isHeadOfHousehold) {
  if (isHeadOfHousehold == true) {
    return true;
  }
  return false;
}
```

Further, the resultant unified function (utilizing a class to return both necessary values) might look like this:

```java
final class taxProfile {
  private final double marginalRate;
  private final int standardDeduction;
  private String[][] itemizedDeductions;
  
  public myTaxProfile(double marginalRate, int standardDeduction, int[] claimedDeductions) {
    this.marginalRate = marginalRate;
    this.standardDeduction = standardDeduction;
  }

  public double getMarginalRate() {
    return marginalRate;
  }

  public int getStandardDeduction() {
    return standardDeduction;
  }
  
  public String[][] claimedDeductions() {
    return claimedDeductions[][];
  }
  
}

...

taxProfile selectTaxRateSchedule(boolean isMarried, boolean isJoint, boolean isHeadOfHouse, boolean isTrustOrEstate, double income) {
  if (marrigeStatus(isMarried) == 1) {
    if jointReturn(isJoint) == 1) {
      deductionLookup(claimedDeductions());
      return new myTaxProfile(findJointMarginalTaxRate(income), 12600, claimedDeductions[][]);
    }
    else {
      deductionLookup(claimedDeductions());
      return new myTaxProfile(findIndividualMarriedMarginalTaxRate(income), 6300, claimedDeductions[][]);
    }
  }
  else if (headOfHousehold(isHeadOfHouse) == 1) {
    deductionLookup(claimedDeductions());
    return new myTaxProfile(findHeadOfHouseholdMarginalTaxRate(income), 9250, claimedDeductions[][]);
  }
  else if (trustAndEstate(isTrustOrEstate) == 1) {
    deductionLookup(claimedDeductions());
    return new myTaxProfile(findTrustAndEstateMarginalTaxRate(income), 0, claimedDeductions[][]);
  }
  else {
    deductionLookup(claimedDeductions());
    return new myTaxProfile(findIndividualMarginalTaxRate(income), 6300, claimedDeductions[][]);
  }
  throw new IncorrectDataException();
}
```

Already, we can begin to see how the layering of simple logic - even repetitive logic - can lead to some very dense and not-so-intuitive code that has to process it all. And, all of this code is made simply to find the right schedule and deductions - there is no actual calculation taking place, since by the end of the `selectTaxRateSchedule()` function we've merely passed a class that contains some of the information needed to calculate the user's tax burden. Furthermore, in isolation it is all but impossible to understand what `selectTaxRateSchedule()` is even doing - though obvious names for functions and variables are used, some values aren't stored (and thus aren't labeled), and the purpose of most of the contained functions remains obscure until they are discovered and inspected.

Hopefully, this helps to illustrate how combining simple rules and churning through them many times can quickly become burdensome for coders and systems alike, making it all prone to bugs if a developer hasn't thought through the myriad of possible outcomes these logical rules introduce at runtime. Even if a developer creates perfectly bug-free code for this logic, in fact, they still have to consider if the rules are written in such a way that, in runtime, they don't utilize more resources than absolutely necessary to find the desired results. In the above code, for example, does it make sense to deduce individual tax filers last, instead of heads of household? Is it prudent to check marital status as a precursor to checking whether or not someone is filing jointly? Is there a reliable means of checking itemized deductions before determining the filing status of the user, that saves on resources at runtime? How would we know?

There are other challenges as well. What if we need to change some of these tax rates? What if we want to modify what ranges are covered by what rates? How about adding new tax brackets entirely? New itemized deductions? In the above example, since all of this logic lives in the application as variables in Java code, we have to have a developer look through the source, find the code, and make changes. We then have to re-test and re-deploy the application. All of this is incredibly time consuming and expensive, even though the change itself is fundamentally quite simple in principle and small in scope.

Well, as you might have figured out by now, all of this (and more) comprise the "problems" that rules engines look to solve.

_(Note that, for the purposes of this path, the BRE (Business Rules Engine) we'll be focusing on is Red Hat's BRMS, which is built upon JBoss Drools, Guvnor, and other open source projects. That said, the concepts behind any rules engine are generally the same.)_

<!-- @section -->

### The benefits and challenges of using a Rules Engine

It may seem unusual at first to effectively outsource intellignece and logic from the application that's using the logic anyway, but abstracting logic from application code provides a variety of benefits:

* For logic that needs to be changed or updated often, it is usually time-consuming and expensive to perfom such updates when the logic is expressed in application code. A developer has to find the code that contains the logic, and then make changes. Those changes have to be tested for QA purposes. And then the updated application has to be deployed. Rules, comparatively, are easier to update, and faster to deploy - even a non-programmer can concievably use the BRMS interface to update rules in real time, and rules can be deployed to live applications without interruption, and without the risk of introducting bugs in the application code.
* Logic expressed in programming languages like Java tend to be difficult to understand, especially for those who aren't programmers. Even a developer can have trouble understanding the context of a logical function within an application if they didn't write it themselves. Business rules, however, have a more legible syntax that is clearer to experienced programmers and BSA's alike. Furthermore, such rules are much easier to understand outside the context of the application that uses it, reducing the risk of programmatic errors.
* As you might expect, administrating rules, and building similar logic across multiple systems, is much easier when business rules and logic are centralized.
* When utilized properly, rules engines can sometimes offer performance benefits to applications by processing logic faster than if the app did it alone. This is particularly true of applications that process data through logic very often - BRE's rely on sophistocated algorithms that deduce the most efficient way to process business rules, whereas most applications that encapsulate logic rely on simpler or clearer code at the expense of efficiency.

Of course, rules engines have burdens associated with them as well, including:

* Additional costs, both direct (purchasing and maintaining the rules engine and associated hardware/platforms) and indirect (the development and training cost to transition logic into the engine, and train employess on how to utilize it).
* Increased complexity, both from a technology environment perspective, and an application development perspective.
* A small risk of slowing down applications, particularly when developers don't leverage the rules engine properly, and/or don't adapt the right mindset when composing rules (_rule creation is very different from application development!_).

Ultimately, however, rules engines can be very beneficial for environments that change rules often, desire faster rules deployment, want more understandable/accessible logic, or manage many rules across a variety of systems.

<!-- @section -->

### What this Outlearn path will cover

This path is intended to provide a high level summary of the process for installing and using Red Hat's BRMS (Business Rules Management System) platform, with some particulars that should be helpful for developers and rules authors alike. That said, much of the high-level information reflects how rules engines in general tend to work, and aren't specific to Red Hat's solution(s).

<!-- @multipleChoice -->

Pop quiz! What's a _rules engine_?

- [ ] An enterprise solution for handling privileges for various accounts.
- [ ] A system that decides what applications to use, and when to use them.
- [X] A system that processes logical operations, and centrally stores such business logic.
- [ ] An injection-based diesel combustion engine that hypothetically meets strict EPA emissions standards.

<!-- @end -->
  
<!-- @multipleChoice -->

Which of the following _is not_ a benefit to using a rules engine?

- [ ] Centralizing business rules makes such logic easier to administrate and modify.
- [ ] Using a rules engine can sometimes speed up how quickly data is processed logically.
- [ ] The syntax of business rules is easier to understand and work with, even for non-programmers.
- [X] Implementing a rules engine simplifies the technology landscape it is a part of.

<!-- @end -->
  
<!-- @multipleChoice -->

Which of the following _is_ a potential pitfall to using a rules engine?

- [X] Rules engines have a high upfront cost and require both training and ongoing learning.
- [ ] Editing rules is harder and more time-consuming than editing application code.
- [ ] A well-implemented rules engine can make various other applications and systems redundant.
- [ ] Rules engines require massive amounts of storage and compute resources to function properly.

<!-- @end -->
<!-- @end -->
