I was inspired to write about this topic while listening to Modern Web podcast. 
Ray Gesualdo is invited in S10E01 to talk about developing APIs, but one small
fact caught my attention: he mentioned they were still working at migrating away from
AngularJS at Salesloft, while having to .

And then I asked myself: how many other teams and organizations are still on
this route of getting rid of a Frontend framework that originally dates back to
2010-2012 and that is out of support for more than one year? I sayed to myself
"hey, we're not the only ones still fighting to deangularize frontend". And yes,
that's a word we invented (to be completely honest, I can't tell if I
invented it, or somebody else on my team. Best not to assume credit).

Let's start with the most important definition of teh day.

> ##deangularize
  /dɪˈaŋɡjʊlərʌɪz/
  1. to rewrite a JavaScript module (file) that has a dependency on AngularJS (i.e. a
     directive, a service, a `$controller` of some sort, or any piece of
     functionality that used dependency injection, the `$inject`) in a way that no trace of
     Angularjs can be found in the new module (file), whilst preserving the
     previous functional and non functional requirements. And by that, I mean
     unit-tests too.

I hope Ray wouldn't mind quoting him in that podcast:

*We were originally on AngularJS. Okay. And we're still in the process of migrating off of that. And what we've had to do through that process, just like you said, it is the natural kind of inclination to say, I will just burn the old thing down, build the new thing, and we'll just switch over. Well, that rarely works that easily. So one of the things that I've learned through the process and now I'm sharing with others as we keep working through this repo and through this migration is you often have to start by making things more complex to make them more simple. [..] We want to bypass that and just say, I just want to get to the clean thing at the end. It's like, okay, I understand that compulsion, but at the same time we need to deliver value to our customers.*

And that's exactly what we did; we had to build more, so that we can start
cleaning up the AngularJS, and hopefully, one day not very far away, we will
be able to eradicate the obsolete framework from `package.json`.
However, I'm not going to talk to you about Frontend
architecture, as I don't have much credit in the solution design of the
migration from AngularJs to Lit, our target ~~framework~~ library of choice.

The goal of my article today is to provide a guideline for Engineering Managers
or Chapter Leads on managing a complex Software migration.
