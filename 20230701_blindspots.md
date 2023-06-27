---
title: "Blind Spots"
date: "July 2023"
excerpt: "as digital systems increasingly replace human interaction how much of our society is being excluded"
---

# Blind Spots
where is the boundary between deliberately not serving people and blindly excluding segments of society

#### TL;DR
> the short version...

---

INTRO / CONTEXT

Earlier this year I visited Arizona on holiday. It was a wonderful opportunity to to catch up with far away family and to experience an entirely new part of the world. Yet this trip was not without a few bumps along the way. Those bumps all stemmed from computerised, business systems. These experiences started a thread of thought that I've been turning over since then.

The process of booking our flights involved speaking to customer support on 3 separate occasions to complete the booking due to obstacles presented online. When we got state side, not having normal mobile phone access[^1] caused all sorts of challenges: recovering our lost luggage[^2], ordering food in a restaurant[^3], communicating with our AirBnb host[^4], trying to use Skype to make calls[^5].

In stark contrast to the impression left by all these dead-end experiences was the sight of Waymo autonomous taxi's driving around Phoenix. A computerised system driving heavy objects at speed through an elevated risk environment. A system with a zero tolerance for unintended consequences, failures, or blind spots. Seeing this begged the question, in software development how good is good enough?


### What is a business system?

Taking a broad view, a business system, and the software that automates aspects of it, is built to serve the goals of a business. Inevitably developing these systems will involve trade-offs based on commercial priorities and compromises imposed by constraints. These factors optimise the system for core business functions and target customer groups at the cost of deprioritising or entirely disregarding others. This is a fundamental reality of commercial enterprise.

Within system development there is a second story, another strata of factors involved. These include human bias, agenda conflict, technical incompetence, and [wayward best intentions, miscommunication or misguided imagination](https://cerebralab.com/Imaginary_Problems_Are_the_Root_of_Bad_Software). Generally speaking, decisions driven by empirical research.

These factors are further magnified as systems become more complex, and are integrated with other systems. The net result is an inevitable grey area between intended business functions and what customers experience.


### The happy path is happy for who exactly?

Seeing the Waymo taxis I wanted to book a ride but I was thwarted. To hail it a Waymo an app is required but it was region blocked. While disappointing I could easily understand this intentional restriction. It is an ambitious system currently in a very limited trial phase. But what about all those businesses with much less ambitious systems that are already generally available and broadly advertised?

Subsequently I discovered that the problems with our flights were primarily due to our journey having 2 legs, involving different carriers. The integration between these carriers systems had many unmarked dead-ends, and I happened to fall into lots of them. Frustrating but [it could have been much worse](https://edition.cnn.com/2022/12/27/business/southwest-airlines-service-meltdown/index.html).

These integrations can often be the gap that users fall into yet very few organisations have the resources to build everything in house hence [integrations are an essential element in achieve business goals](https://snarfed.org/2022-03-10_were-drowning-software-dependencies). In a world increasingly shifting towards digital self-service as a profession software engineers are surely need to shift our self-image from pioneers and disruptors to essential workers. And shift our duty of care accordingly. I expect this will take time but starting a discussion about it is the easiest, best place to start. Consider:

- Older people who did not grow up in our digital world and now feel increasingly excluded by it.
- Neurodiverse people faced with inaccessible systems.
- People whose financial circumstances exclude them from having a smartphone or a credit card.
- Travelling people excluded by region locks.
- People who don't speak our language as their first language.

Providing for every eventuality is not easy, and not cheap. While travelling state side, the problems I encountered were very much first world problems. Yet they were also a great reminder of the impact software development has on real people. I was fortunate to be able find my own way around these obstacles. In every instance the solution involved the human beings those incomplete business systems were built to marginalise.

As [Conways law](https://martinfowler.com/bliki/ConwaysLaw.html) reminds us, an organisation that builds a system typically builds that system in reflection of that organistion. What type of organisation are you working in: Is there anything you can do to influence that organisation to be more inclusive? Or to at least better at sign post the difference between who it serves and everyone else can find an alternate solution.

## Take aways

- Diversity in an open and candid environment is a great strategy to counter blind spots


* Functional behaviour driven by business decisions vs. unintended gaps in complex, multi-service systems

* Business decisions that leave certain use cases unsupported are an economic reality.

* Testing boundaries within complex systems are difficult. Mocking obscures gaps. Full End-2-End testing is equally problematic.

* Not investing in identifying systemic unknowns and at least applying the bare minimum of reliable, user recovery undermines the entire system.

* Failure to do so invites reputation damage, and could give rise to a system increasingly prone to catastrophe.



### References:

- [Blind Spots in Business and Information Systems Engineering](https://link.springer.com/article/10.1007/s12599-019-00587-2)
- [A rise in self-service technologies may cause a decline in our sense of community](https://theconversation.com/a-rise-in-self-service-technologies-may-cause-a-decline-in-our-sense-of-community-201339?utm_source=DenseDiscovery-243)
- [Blind Spots: Cognitive Biases and Systems](https://www.infoq.com/presentations/cognitive-bias/)


---

[^1]: Three customers face [steep roaming charges](https://www.three.ie/roaming/rates/) including €2+ per minute to either make or receive calls, and €5 per MB for data. To compound this [Three has a reputation for badly overcharging roaming customers](https://www.thejournal.ie/three-ireland-plead-guilty-to-data-roaming-debacle-5967600-Jan2023/). Concerned about this I went into a Three store to get their advice. The response "keep your phone in airplane mode until back in Europe!".

[^2]: When our luggage didn't arrive there was no easy way for us to contact the baggage service, short of going back out to the airport. Also there was no way for their third-party, app enabled delivery service to let us know when our bags were on the way. Leaving us stuck in a stay or go conundrum.

[^3]: When out for a dinner we couldn't order because the menu was only available through a QR code. Our server loaned us her phone to place our order.

[ˆ4]: While staying in an AirBnb we couldn't communicate with my host as I couldn't log into my account. It is authenticated via Facebook and their 2 factor authentication requires a code via SMS.

[^5]: Even when on wifi I couldn't setup Skype to make phone calls, the Microsoft authentication emails required to setup the account never arrived before they had already expired.

