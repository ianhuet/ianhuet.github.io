---
title: "RealWorld Quality Engineering P1.2"
date: "August 2023"
excerpt: "Setup a local development environment"
---

# Phase 1.2. - Setup a local development environment
To get this project moving along the product needs to be established. Also, the setup process should be easy to complete, portable, and easily repeated for anyone engineer, regardless of their experience level.

### The Back End
> This codebase was created to demonstrate a backend built with Typescript + Express + Prisma including CRUD operations, authentication, routing, pagination, and more.

Implemented by [Ronan Soares](https://github.com/SeuRonao/realworld-express-prisma/tree/main). Built with NodeJs [Express](https://expressjs.com/) web framework. Database interactions are managed with [Prisma ORM](https://www.prisma.io/).

This recent implementation required very little to get it working:
- Create & configure an `.env.development` file.
- Enable `Cors` for local development.
- Update the Port number to 5101.

### The Database
The above implementation uses the [PostgreSql](https://www.postgresql.org/) relational database for data persistence. Rather than setting this up with a local database server, [Docker](https://www.docker.com/products/docker-desktop/) has been used. It enables the same facility while also being configured in code and highly portable.

Prisma provides a schema and tooling for handling migrations, gretly simplifying the database setup process. Combining this with [Faker](https://fakerjs.dev/) and some simple scripting produces automated seeding for the database, generating a starter data set. Rather than writing this from scratch, ChatGBT was used to do the heavy lifting. Though it took some tweaking this approach was much quicker than writing it manually.

### The Front End
> React + Redux codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the RealWorld spec and API.

Implemented by [King Elisha](https://github.com/gothinkster/react-redux-realworld-example-app/tree/master). Built with React (16.3), Redux (3.6), React-Router (4.1). It has held up surprisingly well, other than a small change relating to the way Promises were referenced, understandable for a codebase first started 7 years ago, there were no other essential changes required to get this working.

- Direct reference Promise, rather than via `global.Promise`
- Migrate from CRA to Vite
- Update the port number to 5100

### Monorepo
A monorepo is used to manage the frontend and backend (and in due course, test) packages. Based on the [Yarn](https://yarnpkg.com/) package managers workspace functionality, [Lerna](https://lerna.js.org/) provides useful tooling to make managing multiple packages super easy.

------

[Next: Phase 1.3. - Setup a deployment pipeline](#)
