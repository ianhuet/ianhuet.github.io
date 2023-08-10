---
title: "RealWorld Quality Engineering P1.2"
date: "August 2023"
excerpt: "Setup a local development environment"
---

# Phase 1.2. - Setup a local development environment
To get this project up off the ground it's time to get 

### The Back End
> This codebase was created to demonstrate a backend built with Typescript + Express + Prisma including CRUD operations, authentication, routing, pagination, and more.

Implemented by [Ronan Soares (SeuRonao)](https://github.com/SeuRonao/realworld-express-prisma/tree/main). Built with NodeJs [Express](https://expressjs.com/) web framework. Database interactions are managed with [Prisma ORM](https://www.prisma.io/).

As this implementation is so recent there was very little required to get this working.
- Create & configure an `.env.development` file.
- Enable `Cors` for local development.
- Update the Port number to 5101.

### The Database
The above implementation already decided on the relational database [PostgreSql](https://www.postgresql.org/) for data persistence. Rather than setting up a local database server, [Docker](https://www.docker.com/products/docker-desktop/) provides the same facility while also being configured in code and extremely portable. 

Prisma provides a schema which can be migrated into the newly created database. While the schema has not been changed, Faker has been used to create a `seed.ts` for seeding the database with an automatically generated starter data set. Rather than writing this from scratch, based on the schema, ChatGBT did most of the heavy lifting. Though it took some tweaking this approach was much quicker than writing it manually.

### The Front End
> React + Redux codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the RealWorld spec and API.

Implmented by [King Elisha](https://github.com/gothinkster/react-redux-realworld-example-app/tree/master). Built with React (16.3), Redux (3.6), React-Router (4.1) and it has held up remarkably well. Other than a small change relating to the way Promises were referenced, understandable for a codebase first started 7 years ago, there were no other essential changes required to get this working.

- Direct reference Promise, rather than via `global.Promise`
- Migrate from CRA to Vite
- Update the port number to 5100

### Monorepo
A monorepo is used to manage the frontend and backend (and in due course, test) packages. Based on the [Yarn](https://yarnpkg.com/) package managers workspace functionality, [Lerna](https://lerna.js.org/) provides useful tooling to make managing multiple packages super easy.

------

[Next: Phase 1.3. - Setup a deployment pipeline](#)
