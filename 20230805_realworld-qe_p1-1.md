---
title: "RealWorld Quality Engineering P1.1"
date: "August 2023"
excerpt: "Identify a fully integrated project to work with"
---

# Phase 1.1. - Pick the Product

To approach the decision of picking an existing product to focus this project on I set these considerations: open source, client/server w/ database architecture, solid technology stack, reasonably functional, room for improvement.

### a. Open Source
This is an obvious and essential condition as any proprietary technology in the product stack would be an obstacle to writing about here. How this relates to the deployed environment though I am not yet entirely clear, but I am comfortable to leave that decision til later in this phase.

### b. Client/Server w/ Database Architecture
I have worked with different architectures but I am currently most familiar with this arrangement. Sticking with what I am most familiar with will enable me to invest more effort in the quality engineering aspect of the project. In the same vein, looking for a React based frontend and a NodeJs based backend will offer the most candidate projects to choose from.

### c. Solid Technology Stack
If Typescript hasn't already been used on both the frontend and backend would offer an obvious opportunity for improvement but applying that has a potentially bigger footprint than I'd like to bring into the scope of this project. To hone down the range of potential data handling technologies, and to keep it most broadly typical, it should be a relational database. Within this there are a few clear candidates MySql/MariaDB or Postgres. An ORM with migration management would be appealing, and could be useful for seeding the database. And nothing annoying like TailwindCSS either.

### d. Reasonably Functional
Without attaching some crititeria to this it could easily become the vaguest consideration. A CRUD product is a typical application type, though something more functional could be appealing. Authentication is a typical product feature and an interesting dimension to challenge the test strategy.

Beyond this I want a selection of user journeys, encompassing a variety of views. It should also be in a satisfactory state already. Having to spend time fixing existing bugs is an exercise in improving product quality, but not the type of effort I want to be be spending to get the project off the ground.

### e. Room For Improvement
In balance to the previous consideration, I do not want the selected product to be too perfect. As a challenge of the implemented test strategy there needs to be opportunities to further develop the product. This could be package upgrades, code refactoring, or new feature development.

## Product Selection
While reviewing a selection of products I remembered the [Go Thinkster RealWorld](https://github.com/gothinkster/realworld) project a.k.a. [the mother of all demo apps](https://medium.com/@ericsimons/introducing-realworld-6016654d36b5). The intention of that project is to provide a meaningful context for interested folks to explore any web application development technology they want. The project creators established an [API schema](https://github.com/gothinkster/realworld/blob/main/api/openapi.yml) and made an implementation of both the front and back publicly available. From this anyone is free to explore an implementation however they want; front-end, back-end or fullstack.

For me this offers a [feature rich CRUD application](https://www.realworld.how/docs/implementation-creation/features), without being overbearing, and [a wide selection of implementations to pick from](https://codebase.show/projects/realworld). I originally had it in mind to find a more complex application type. On reflection this more generic application type presents sufficient challenges. To that end, I chose to go with a mix of [a modern backend](https://github.com/SeuRonao/realworld-express-prisma/tree/main) and [a prehistoric frontend](https://github.com/gothinkster/react-redux-realworld-example-app/tree/master). Disregarding my earlier notion to work with a product that is already entirely Typescript.

------

[Next: Phase 1.2. - Setup a local development environment](20230805_realworld-qe_p1-2)
