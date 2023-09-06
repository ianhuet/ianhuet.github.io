---
title: "Rigour over Routine"
date: "September 23"
excerpt: "Critical thinking is more useful than better tooling"

---

# Rigour over Routine
Rigour over Routine

#### TL;DR
> For the first time in a long while a side project brought me back to website development. It was great to see how much of the tooling has advanced. Yet I wonder do these tools enable greater productivity today at the expense of empowering greater engineers tomorrow? I think it depends on critical thinking.


---

I recently replatformed a simple portfolio/blog website. Originally built with [Gatsby](https://www.gatsbyjs.com/), and populated from content stored in markdown files updated via a GitHub. I chose to use [NextJs](https://nextjs.org/) to migrate the otherwise unchanged frontend over to. However, arriving at a satisfactory, entirely UI based CMS[^1] backend I had to go through several iterations[^2].

## Reflections
While it took several iterations the availability of a broad range of functional tooling. In terms of potential productivity this was great to see. However I felt a lurking doubt amongst all the hype and claims to grandeur.

- great tooling, abstractions a-go-go
- what level of ability is lost in this abstraction

## Configuration Over Configuration
  - DHH & Rails
  - Pros, cons, etc.
    + Setup / Functionality for free
    + Patterns in Practice
    - Can appear magical, challenging for uninitiated engineers to adopt
    - Vendor lock-in
    - Abstraction of Learning: can easily result in a focus on how something works rather than why something is setup to work in 

-> Critically: serves majority over specifics
  ? Hopefully lots of customisations

- Reflection:
  - software development is not easy or cheap. at best it is an expensive value-centre, otherwise it is a cost-centre drag
  - driven by these economics, it is inevitable that no-code & AI based code generation is going to become more capable
  - in this context, beware a dependency on the conventions you know becoming the hammer you hit every problem with
    - surely you'll be replaced by a robot
    + learn how to better use many tools

- ** in the long term, productivity is no subsititute for critical thinking. Pragmatic Engineer article.

- ** in the the meantime, thanks Vercel & Sanity for helping me ship a simple portfolio/blog website fast & free


## Take aways

- practice til you are competant in delivering with one tool stack

- then do not become dependant on that stack for your livlihood, actively explore alternatives

- honing your critical thinking is the secret ingredient to a long and productive career


### References:

- [Is Critical Thinking the Most Important Skill for Software Engineers?](https://blog.pragmaticengineer.com/critical-thinking)

https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/patterns-in-practice-convention-over-configuration
https://visionedgemarketing.com/marketing-from-cost-center-to-value-center
https://techstacker.com/frameworks-convention-over-configuration


## Video

https://www.youtube.com/watch?v=uVtXNNmvYwg
https://www.youtube.com/watch?v=f-4YrioKo6U

---

[^1]: Content Management System ([CMS](https://en.wikipedia.org/wiki/Content_management_system))

[^2]: **Replatforming Iterations**

My first goal was an authenticated and functional CMS that could be easily deployed. From that point I intended to incrementally adapt it to requirements. In search of this foundation I took the low effort approach of seeking out tutorials, with a low tolerance for obstacles:

### Candidate #1 - Vercel Postgres database
[How to Build a Fullstack App with Next.js, Prisma, and Vercel Postgres](https://vercel.com/guides/nextjs-prisma-postgres)

As the frontend was going to be hosted with Vercel exploring the options they provide seemed like a logical place to start. Thankfully migrating the frontend from Gatsby to NextJs was straight forward. Though the tutorial did not use the new [App Router](https://nextjs.org/docs/app) which needed to be adapted.

Then this undated article's atrophy showed itself again. Installing NextAuth@latest to add authentication functionality it became clear that it had a different API than the one expected in the article. Unfortunately the expected version was not documented, and it proved too time consuming to identify. Time to move onto the next candidate.

### Candidate #2 - PayloadCMS w/ MongoDB
[](https://blog.logrocket.com/using-payload-cms-build-blog/)

Among a broad range of available CMS services this was a strong option. It proved to be super easy to setup & customise. Genuinely a pleasure to work with however the fact that it only works with MongoDB was a deal breaker, as I could not readily find a free provider.

Though it is worth noting that [more database adaptors are on their way](https://payloadcms.com/blog/relational-database-table-structure-rfc).

### Candidate #3 - Sanity CMS platform
[](https://www.sanity.io/blog/build-your-own-blog-with-sanity-and-next-js)

I tried Sanity.io next. Following this recently updated article, built on the generous free tier offered by Sanity, everything just worked. Sanity really do have their user/developer experience offering well honed! Solution found \o/