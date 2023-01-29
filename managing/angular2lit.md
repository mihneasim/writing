I was inspired to write on this topic while listening to Modern Web podcast. 
Ray Gesualdo is invited in S10E01 to talk about developing APIs, but one small
fact caught my attention: he mentioned they were still working at migrating away from
AngularJS at Salesloft, while having to support the business requirements and
the continuity of the service to the customers.

I then asked myself: how many other teams and organizations are still on
this route of getting rid of a 2010-2012 Frontend framework
that is out of support for more than one year? I told myself
"hey, we're not the only ones still fighting to *deangularize* frontend". And yes,
that's a word we invented (to be completely honest, I can't tell if I
invented it, or somebody else on my team. Best not to assume credit).

Let's start with the most important definition of teh day.

> **deangularize**
>
>  /dɪˈaŋɡjʊlərʌɪz/
>
>  1. to rewrite a JavaScript module (file) that has a dependency on AngularJS (i.e. a
     directive, a service, a `$controller` of some sort, or any piece of
     functionality that used dependency injection, the `$inject`) in a way that no trace of
     Angularjs can be found in the new module (file), whilst preserving the
     previous functional and non functional requirements. And by that, I mean
     unit-tests too.

I hope Ray wouldn't mind quoting him in that podcast:

*We were originally on AngularJS. Okay. And we're still in the process of migrating off of that. And what we've had to do through that process, just like you said, it is the natural kind of inclination to say, I will just burn the old thing down, build the new thing, and we'll just switch over. Well, that rarely works that easily. So one of the things that I've learned through the process and now I'm sharing with others as we keep working through this repo and through this migration is you often have to start by making things more complex to make them more simple. [..] We want to bypass that and just say, I just want to get to the clean thing at the end. It's like, okay, I understand that compulsion, but at the same time we need to deliver value to our customers.*

And that's exactly what we did; we had to build more, so that we can start
cleaning up the AngularJS and hopefully, one day, not very far away, we will
be able to eradicate the obsolete framework from `package.json`.
However, I'm not going to talk to you about Frontend
architecture, as I don't have much credit in the solution design of the
migration from AngularJs to Lit, our target ~~framework~~ library of choice.

The goal of my article today is to provide a guideline for
Chapter Leads (or Engineering Managers) on managing complex Software migration.
On making them happen.

1. Find the right talent.
1. Secure their environment.
1. Remove non-engineering impediments.
1. Ship and remove uncertainties.
1. Sell it to stakeholders & Scale it to contributors.
1. Measure progress and show it off.

## 1. Find the right talent

Just as managers have their own "managerial style", so are engineers. While
feedback collection is always a good idea, democratic government in migration
strategy implementation just isn't.

| **Validate as a team**                 | Migration strategy                 |
|----------------------------------------|------------------------------------|
|  **Dedicate to one expert individual** | Migration strategy implementation  |

If you want the migration done properly, you will need to pick one engineer and stick
to his or her style. I haven't been in this situation, but if you feel you made
a wrong choice, it's probably best to pivot at this step. **Picking the right
talent is the most important choice**; anything else can be figured out later.

## 2. Secure their environment

You want this engineer to have focus. Make this demand clear to the stakeholders from the
start and ask for commitment. Product people need to be fully onboard and
understand big migrations require focus at the very start. The
engineer can not be troubled with other work; we have the rest of
the frontend chapter to accommodate the *run* and the other *change* parts 
of the product delivery of the tribe. This is where a solid team comes into play: it allows for one
individual to step aside from the delivery spree, without affecting the tribe
deliverables.

It goes without saying the migration work would be captured in a squad's backlog, but the
key idea here is **The appointed engineer should have focus to come up with the
migration implementation plan**.

For me, it was easier to secure this environment in the recruitment phase.
Since the individual was by any mean a new joiner, there were no past activities to close down or to hand over.
No ties to break.
I made sure to make it transparent to the Product (to the Tribe Lead) that we wanted
to onboard the next new engineer specifically for the migration kick-off. In my
case, the candidate showed strong proficiency and growth potential,
so it really made sense to offer him a matching growth opportunity.

## 3. Remove non-engineering impediments

Part of the engineering focus mantra, best thing a lead can contribute with here is
handling, personally, any organizational impediments. Here's where a Chapter
Lead wears multiple hats:
 * of an architect, by communicating the migration project to the tribes
 * of a product manager, aligning development, testing and deployment schedules
 * of a release manager, by drafting the release form, documenting the change
   and getting it approved

## 4. Ship and remove uncertainties

Your change will have a high amount of risk. Migrating from one legacy frontend
stack to something modern will require having both of them work together for a
long time, until the final steps of the migration.
It will be messy. Things will break, in all phases, and hitting production won't
make an exception no matter how much you prepare.

In Frontend it is way more simple to manage an Alpha / Pre-Production
environment that you can run in the public internet.
Have it run on the devices of some of your designated beta
testers. Test it on your laptop, test it on your phone. Use it for a week. Are
there routing problems, navigation issues? Data retention, is the old framework
still correctly rendering on data changes? Is the new one sharply bootstrapped?

Your engineer should make sure the high-risk high-impact uncertainties are
asserted first during these Alpha-releases.
You, as a lead, should support these releases with all the *hats* that are
needed. In banking, we are equally careful with alpha releases as we are with
any release to our customers. Even if it's an alpha version, rolled out to a subset of
customers, or even internal employees, we still need to deliver a secure,
major-incident-free frontend app.

At the end of this step is where the solution takes place. It's the ***It Works!***
tears-of-joy kind of feeling. It's where all the assumptions are either validated,
or mitigated by pivoting until we get a working plan.
A working way-of-working where we can enable squads to start building and
shipping in the new stack, little by little. Until we can finally extract the
old stack (AngularJs) from the application shell.

Our solution, in a nutshell, meant an implementation of the strangler pattern,
where we migrate to `lit` one customer journey (feature), after another,
leaf by leaf, and ship it incrementally to production. We were able to build
and **validate** recipes like:

 * Convert an AngularJs service to an es6 module with a vanilla class,
   that would export one instance of it (always the same; singleton pattern).
 * Substitute Dependency Injection with es-imports and spies (for tests)
 * Have each migrated journey configure and instantiate its own router, that
   would hook up into the ui-router of AngularJs for the legacy route

## 5. Sell it to stakeholders & scale it to contributors.

The first thing you ship to production, will most definitely:
 - be more bulky in filesize (containing both legacy, and the modern stack)
 - look the same
 - behave the same; it will have marginally the same non-functional attributes
 - **but** it will enable teams to start building frontend features in a modern
   target stack

That will need to come through in your message to the stakeholders: to the tribe
lead and to the product owners of each of the squads that deliver frontend.

List out some low-hanging fruit selling points, but also draw a mid and long
term plan, i.e.:
 1. Are there new components or experiences shortly enabled for UX architects to
    include in their future designs?
 1. Is there a vulnerability that will be addressed incidentally by the migration?
 1. Will we ship faster in the newly enabled stack?

## 6. Measure progress and show it off.

Measuring migration progress is not an easy task, but its role is critical,
helping:
 * to be able to compare one module to another
 * to evaluate the costs and take decisions
 * to keep the momentum and the motivation

I have classified migration metrics in two categories.

### A. Quantitative metrics

Although misleading and often non-linear with complexity and migration effort,
the quantitative metrics have the advantage of being objective and instantly
measurable. It's the stopwatch that never lies.
Pick one, two or more legacy framework *traces* that can be measured across
the codebase. For AngularJs, you can measure the number of angular.modules,
services, providers, components, directives, constants.

However, the most relevant and merciless metric we could think of was the number
of *injection occurrences*. That's right, what is the total length of all Arrays
of `$inject`-ed identifiers in the project?

When we started out, we counted about 60 customer journeys to migrate, made up
of about [...numbers...]

### B. Qualitative metrics


