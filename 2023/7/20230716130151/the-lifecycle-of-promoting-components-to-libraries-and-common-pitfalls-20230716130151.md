---
path: '/2023/7/the-lifecycle-of-promoting-components-to-libraries-and-common-pitfalls-20230716130151'
title: 'the lifecycle of promoting components to libraries and common pitfalls'
date: '20230716130151'
category: 'libraries'
tags: ['components', 'modules', 'libraries', 'lifecycle', 'code hygiene']
---

# the lifecycle of promoting components to libraries and common pitfalls
I see quite a few bad code smells in the management of library components.
These are usually pretty quick to spot, and I think that most people writing or reading
lots of code will see a few explanations of my thought process and say "oh, okay, yeah".

However, when applying these thoughts to our daily programming practices it is a little
tricky to weigh in against:
* Time deadlines
* "Good enough" software (thanks [Software Craftsmanship](https://www.thriftbooks.com/w/software-craftsmanship-the-new-imperative_pete-mcbreen/1014053/))
* Reducing complexity (which is usually our goal)

## Laying the groundwork - How i'm level setting the scene for discussion
When discussing libraries I want to be sure that it's clear we're discussing portions
of code designed for an application (to do something, problem 1) that we want to also apply
to something else (a 2nd problem).
* `Problem 1` - The reason the original code was written
    * A general list of constraints is good to have
    * Working code, in hand, can solve this problem already
* `Problem 2` - A similar, closely related problem with a general "workflow" of the same logic
    * Constraints may differ (ex: values in variables being different)
    * The problem may have additional complexity, but have similarities in "core" logic but
    maybe has a few extra edge cases
    * This lives within the same code base as `Problem 1`.
        * Do not abstract to a separate project to solve the same/similar problem, if possible. See below.

### Defining terms
* Core lib -
    * Used by business logic or middleware between services
    * Client interfaces that are domain specific
* Installable -
    * Spans several domains
    * Is small (initially, most of the time)
    * Is general enough to be used by **multiple *different*** things
    * Is complex enough to not copy + paste and duplicate (stop being so allergic to this)
    * Is worth the overhead of:
        * Releasing our library separate from our application code
        * Updating our app's release every time we change this 3rd piece of code living somewhere else
        and ebuilding our app!
        * Rinse and repeat

### Example libraries
* Installable - Good first examples that teams need!
    * Config parsers that load a `.json` file standard we share across our team's projects
    * Logging output handlers that keep a consistent format across our team's projects
    * Database clients - A shared library of some way to connect to and execute queries on databases
        * Create these with caution :)
* Core lib - These live inside your application (ideally in your mono repo...)
    * Terraform (infrastructure as code) or other modules with strict adherence to a "standard"
        * Ex: Our team uses Terraform workspaces so all our modules use this standard.

## The lifecycle of a component
This lifecycle (in my eyes) of course has flexibility at each stage for the "size" of
code, substitute "function" at step #1 for any: existing library, feature, 10 modules, etc.

### Outlining the evolution of the code
1. Core library function - (`Problem 1`)
    1. Used as a proof of concept initially
    1. Is adopted into a feature to determine some new capability or solve a problem
    1. This would be the "fast and dirty" approach that we later clean up, maybe we
    spend a long time making it work very well and defining edge cases.
    
1. Interface or "client" or "tool" - Whatever term you'd like to use for a single
entrypoint that can end-to-end execute your previous code (`Problem 1`) in a "general" interface

    1. We want to abstract the code to take multiple cases (`Problem 2`)
    1. This lives side-by-side in our same codebase with `Problem 1`
    1. Think about the structure of "how does this live side-by-side" my existing code?
    1. **Note:** You want to change logic in isolation, solve each problem first then abstract
        1. Just copy paste the code initially, please. Don't abstract it yet. Get both problems to be solved first.
    1. Keep in mind this likely contains business logic still, which we want to remove from our
    component as it gains complexity (and features).
    1. **Do not abstract to a separate codebase:** In this example you would create 3 code bases to
    maintain separately if you were to abstract into a new project.
        1. `Codebase 1` - `Problem 1`
        1. `Codebase 2` - `Problem 2`
        1. `Codebase 3` - `Solution 1 & 2`

1. Spread the interface to more domains - We want this used in other areas, by other people, to spread
our influence and cool feature. This feature has solved `Problem 1` and `Problem 2` now, let's expand
it to see if:

    1. A portion of it can be generalized to a shared location for other, closely related problems can share
    1. The component might be considered a "module" with several moving parts, ensure these
    have "guardrails" as the code is used in more contexts:
    
        1. Are parameters properly validated with `ValueError` or similar exceptions?
        1. Can users read your documentation in the function strings and file headers to
        get an idea of what you want to accomplish?
        1. Is the code well formatted?
        1. Do we have a comment somewhere defining the value this brings, what its intent was,
        and any pitfalls?
        1. Is there a `TODO` with the intentions from the author for any future expansion?

    1. Would other problems unrelated to the "business logic" of this feature be benefitted
    by having access to some/all of this code?

        1. **Note:** It is important to remember a library can be as small as 1 function,
        so we can always splice out the business logic specific to our app into a sub-function/component/whatever
        and only "ship" the parts we want to be installable.

1. Make a library that can be installable - If the component has reached this stage, it is ready to be created

## Common pitfalls
These are some of the less refined "ergonomics" I've seen in other development environments.
* A library of libraries is bad - We don't need our project to be 10 libraries that we
create a web of self-installations to "install" our software "in our app", that's bad.
    * Just package the code into your runners, please.
    * Break this into a mono repo or condense to a mono-lib/core-lib that is installable everywhere.
* Not setting library standards and allowing scope creep
* Improperly handling edge cases of other components, then recreating the solution
in a new project
* Creating libraries for the sake of "reducing code repetition"
    * Why are you going through all this effort to generalize when you haven't even finished implementing the 2nd problem?
    * Don't create a 3rd project when you only have 2 problems.
    * If it is truly a separate project, copy paste the code and generalize later. You'll want to fix things,
    doing so with the weight of a library to "keep it backward compatible" is bad.
    * You want to change logic in isolation, solve each problem first then abstract
    rather than creating (more) problems by trying to solve 2 problems at once (abstraction + `Problem 2`)
