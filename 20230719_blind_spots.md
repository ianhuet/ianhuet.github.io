---
title: "Blind Spots"
date: "July 2023"
excerpt: "as digital systems increasingly replace human interaction the duty of care required of system developers must increase also"
---

# Blind Spots
As digital systems increasingly replace human interaction the duty of care required of system developers must increase also.

#### TL;DR
> Computerised self-service systems are increasingly replacing human interaction. Though this enables businesses to scale it also increases the likelihood of introducing blind spots into those systems. Without taking a systematic approach to managing this customers will suffer, especially non-typical customers. 

---

Earlier this year I visited Arizona on holiday. It was a wonderful opportunity to catch up with far away family and to experience an entirely new part of the world. While it was a great trip it also presented some unexpected obstacles. Reflecting on these has been a welcome reminder to consider the broader, potential impact of system development decisions.

To complete booking the flights involved speaking to customer support on 3 separate occasions due to obstacles presented online. When I got state side, not having normal mobile phone access[^1] caused all sorts of challenges: recovering our lost luggage[^2], ordering food in a restaurant[^3], communicating with our AirBnb host[^4], trying to use Skype to make calls[^5]. Integrated, computerised business systems were the common thread through all of these challenges.


### What is a business system?

Stepping back a moment, a business system, and the software used to automate aspects of it, is built to serve the goals of a business. Inevitably developing these systems will involve trade-offs based on commercial priorities and compromises imposed by constraints. These factors optimise the system for core business functions and target customer groups at the cost of deprioritising or entirely disregarding others. This is a fundamental reality of commercial enterprise.

Within this there is a second story, another strata of factors. These include human bias, agenda conflict, technical incompetence, and [wayward best intentions, miscommunication or misguided imagination](https://cerebralab.com/Imaginary_Problems_Are_the_Root_of_Bad_Software). Generally speaking, [decisions not driven by empirical research](https://www.uxdesigninstitute.com/blog/user-research-in-ux-design/).

These factors are further magnified as systems become more complex, and are integrated with other systems. The net result is an inevitable grey area between intended business functions and what customers experience.

In stark contrast to the impression left by all those dead-end experiences was the sight of Waymo autonomous taxi's driving around Phoenix. A computerised system driving heavy objects at speed around public spaces. A system with a zero tolerance for unintended consequences, failures, or blind spots. Seeing this begged the question, in software development how good is good enough?


### Who does the happy path serve?

Seeing the Waymo taxis I wanted to book a ride but I was thwarted. To hail it a Waymo an iOS/Android app is required but I found it was region blocked. While disappointing I could easily understand this intentional restriction. It is an ambitious system currently in a very limited trial phase. But what about all those businesses with much less ambitious systems that are already generally available and broadly advertised?

Subsequently I discovered that the problems with booking the flights was primarily due to our journey having 2 legs, involving different carriers. The integration between these carriers systems had many unmarked dead-ends, and I happened to fall into lots of them. It was frustrating but during the time I was travelling [it could have been much worse](https://edition.cnn.com/2022/12/27/business/southwest-airlines-service-meltdown/index.html).

These integrations can often be the gap that users fall into. [Building the entire system in-house could help to mitigate this for a period but very few organisations have the resources to do this](https://snarfed.org/2022-03-10_were-drowning-software-dependencies). Consequently, in a world increasingly shifting towards digital self-service these grey areas are becoming more prevalent. While [the potential impact of this on society is not yet clear](https://theconversation.com/a-rise-in-self-service-technologies-may-cause-a-decline-in-our-sense-of-community-201339?utm_source=pocket_saves), outcomes off the happy path are also more likely.

In systems built to send rockets into space or to enable autonomous cars ignoring these scenarios are not acceptable. Yet so many other widely available systems are not built to this standard. With the increasing impact this has on peoples lives it is high time to shift our duty of care, both for the sake of our customers and to mitigate the potential reputational impact of not doing it.

Of course, covering every eventuality is not easy, and not cheap. While travelling state side, the problems I encountered were inconvenient but not critical. Yet they were also a great reminder of the impact software development has on real people. For teams building these systems periodoic discussion is the easiest, best place to start - a regular touch point to reinforce who these systems are being built for. Time to consider who you do and do not serve, then be up-front about it. 

As [Conways law](https://martinfowler.com/bliki/ConwaysLaw.html) states, an organisation that builds a system typically builds that system in reflection of itself. What type of organisation are you working in: Is there anything you can do to influence that organisation to be more inclusive? Or to at least sign post who it serves so everyone else can save their energy for finding an alternate solution.


## Take aways

- Clear business direction in terms of available resources and setting acceptance parameters is vital to establishing alignment between business priorities and engineering teams.

- Rigorous end-2-end testing, especially across integrations, is essential to identifying potential problems.

- Not investing in the systemic identification of system  unknowns and at least applying the bare minimum of reliable, user recovery inevitably undermines user confidence in the entire system.

- In our system development teams, diversity in an open and candid environment is a solid strategy to counter blind spots.

- Failure to do so invites reputation damage, and contributes to a system increasingly prone to catastrophe.


## References

[Blind Spots: Cognitive Biases and Systems](https://www.infoq.com/presentations/cognitive-bias/)

[Don’t Get Blindsided by Your Blind Spots](https://hbr.org/2020/11/dont-get-blindsided-by-your-blind-spots)

---

[^1]: Three customers face [steep roaming charges](https://www.three.ie/roaming/rates/) including €2+ per minute to either make or receive calls, and €5 per MB for data. To compound this [Three has a reputation for badly overcharging roaming customers](https://www.thejournal.ie/three-ireland-plead-guilty-to-data-roaming-debacle-5967600-Jan2023/). Concerned about this I went into a Three store to get their advice. The response "keep your phone in airplane mode until back in Europe!".

[^2]: When our luggage didn't arrive there was no easy way for us to contact the baggage service, short of going back out to the airport. Also there was no way for their third-party, app enabled delivery service to let us know when our bags were on the way. Leaving us stuck in a stay or go conundrum.

[^3]: When out for a dinner I couldn't order because the menu was only available through a QR code. Our server loaned us her phone.

[ˆ4]: While staying in an AirBnb I couldn't communicate with the host as I couldn't log into my account. It is authenticated via Facebook and their 2 factor authentication requires a code via SMS.

[^5]: Even when on wifi I couldn't setup Skype to make phone calls, the Microsoft authentication emails required to setup the account never arrived before they had already expired.
