---
title: "Global vs. Server State"
date: "23 June 2023"
excerpt: "Must there be global state for everything?"
---

# Global vs. Server State
Within a client-side app, can the creation & maintainence of global state be automated away without loosing capabilities?

### TL;DR
> Is there a easy-to-use, automated way to handle read-only server data on the client-side without building global state? I created a simple application in both Vue3 & React to investigated this. Using Apollo Client to connect with the same GraphQL API in both apps, the ability to do fine-grain cache querying in React presents a significant advantage. For now Vue@3 still requires a client-side global store to achieve the same functionality.

---

A client's project is built with Vue@2, Vuex, Apollo Client & GraphQL. Coming from a React background, I thought this stack would enable the automated handling of server state. During a recent discussion I queried why Apollo Client caching was not being used in this way, instead of using Vuex to store all server data. The response was that it was not possible. To sense check my thoughts around this I created a simple application in both Vue3 & React to compare capabilities.

**Technical Context:**

The client/server architecture of SPAs[^1] neccessitates all server data be transmitted to the client. Tools like Vuex or Redux are then used to cache this data as global state, to reduce the latency penalty this pattern incures. This has several benefits: after the client buffer is primed it creates a perceived UI performance improvement, it removes the need for prop drilling, data can be accessed rather than copied, as well as acting as a communciation bus - potentially connecting separate aspects of an app.

Global state is the generic name for this client-side data store. The bucket that both a clients app state and all that server persisted data are dropped into. While the mentioned benefits are handy this approach also adds complexity, and an on-going maintenance overhead. Further more it handles these different data types, with their different characteristics, in the same way. This is extra work for a suboptimal solution.

Can this client data and server data be broken up for a better outcome achieved with less work?

### Application Outline

1. Use the same, existing GraphQL API - [star-wars-swapi@current](https://studio.apollographql.com/public/star-wars-swapi/variant/current/home).
2. Use a router to enable both a List & Detail view of the available data.
3. Using Apollo Client, how much can be achieved in React & Vue@3 without using global state?

## Iterations

## [Vue v.1](https://github.com/ianhuet/vue-server-state/tree/c69e9d922c126fbdc9a426203bad37084e12abbf)

1. Using [Apollo Studio](https://studio.apollographql.com/public/star-wars-swapi/variant/current/explorer) makes exploring the API simple, and just as easy to create GraphQL queries.

2. These queries were then [copied across to the application](https://github.com/ianhuet/vue-server-state/blob/c69e9d922c126fbdc9a426203bad37084e12abbf/src/queries/index.ts), and wrapped with `graphql-tag` to enable GraphQL to parse those queries.

3. `@vue/apollo-composable@4.beta` is a Vue wrapper around `@apollo/client@3.7.15`. It provides a 'hook' style abstraction for making requests. Using this [makes the whole data request lifecycle super, straight forward](https://github.com/ianhuet/vue-server-state/blob/c69e9d922c126fbdc9a426203bad37084e12abbf/src/views/ListView.vue).
```typescript
const { result, loading, error } = useQuery(queries.listFilms)
```

4. Setup `@graphql-codegen/cli` to [generate Typescript types](https://github.com/ianhuet/vue-server-state/blob/c69e9d922c126fbdc9a426203bad37084e12abbf/codegen.yml) from the defined GraphQL queries, and [apply them to add type-safety](https://github.com/ianhuet/vue-server-state/blob/c69e9d922c126fbdc9a426203bad37084e12abbf/src/views/DetailView.vue#L16C43-L16C43).

## [React v.1](https://github.com/ianhuet/react-server-state/tree/main)

Firstly, recreate everything implemented in the Vue app. Then try to improve on several aspects:

1. Refactor queries using fragments, extracting portions of the queried data that are reuseable. This fragmention has the added bonus of enabling the [use of cache querying](https://github.com/ianhuet/react-server-state/blob/main/src/components/Production/Production.tsx) with the Apollo Client `readFragment` method. As sections of the cached data can now be directly accessed this removes the need for prop drilling.
```typescript
const production = client.readFragment({
  id: `Film:${id}`,
  fragment: fragments.filmProduction,
});
```

2. Review the GraphQL codegen configuration as manually applying the generated types is tedious. In place of `graphql-tag` [the codegen process generates its' own template literal tag](https://the-guild.dev/graphql/codegen/docs/guides/react-vue#writing-graphql-queries) for parsing GraphQL queries. Switching this over achieves the same functionality while also automatic applying the types generated from the queries to the responses.
```typescript
import { gql } from '../generated/gql';
```

3. Apollo Client enables individual field data decorators, [applied via a Type Policy on the cache configuration]((https://www.apollographql.com/docs/react/caching/cache-field-behavior)). Applying this [type policy on the cache](https://github.com/ianhuet/react-server-state/blob/main/src/main.tsx) enables the transformation of individual data points as they are received, upstream of any use within the application.
```typescript
const cacheConfig = {
  typePolicies: {
    Film: {
      fields: {
        releaseDate: {
          read(releaseDate: string): string {
            const date = new Date(releaseDate);
            return `${date.getDate()} / ${date.getMonth() + 1} / ${date.getFullYear()}`;
          }
        },
```

4. If navigating to a Film Detail view from the Film List view there is cached data that can be presented [while loading the `FilmDetail` query](https://github.com/ianhuet/react-server-state/blob/main/src/pages/DetailView/DetailView.tsx). This is enabled by passing the cached `FilmProduction` fragment across with the navigation, using the [react-router-dom data APIs](https://reactrouter.com/en/main/hooks/use-loader-data).
```typescript
const film = {
  ...cache,
  ...data?.film,
}
```

5. Using the cache in this way can be extended with [local fields](https://www.apollographql.com/docs/react/local-state/managing-state-with-field-policies), custom fields added on the client-side and queryable with any of the cached server state. Though a [local schema](https://github.com/ianhuet/react-server-state/blob/main/schema.local.graphql) is required to integrate local fields with the automatically generated types.
```typescript
extend type Film {
  episodeIdNumeral: String
}
```

## [Vue v.2](https://github.com/ianhuet/vue-server-state/tree/main)

Time now to see how many of this enhancements can be ported to the Vue app... 

1. Reconfigure `@graphql-codegen/cli` to use in place of `graphql-tag`, enabling the automatic application of type-safe on requests.
2. Add a [client-side local field](https://github.com/ianhuet/vue-server-state/blob/main/src/main.ts) and add it to the generated types using a supplimentary [local schema](https://github.com/ianhuet/vue-server-state/blob/main/schema.local.graphql).

## Take aways

- Getting up & running in either VueJs or React was super simple using `npm create vite@latest`.
- Taking full advantage of `@graphql-codegen/cli` enables automated type safety on request responses.
- Apollo Client greatly improves the API request process by both simplifying the request lifecycle, and automatically caches all response data in a queryable manner.
- Apollo Client offers the ability to augment this data store with local fields, and per field data decorators.
- In React, Apollo Client further enables fine-grain querying of that data cache.
- The `@vue/apollo-composable` wrapper package enables the simplified request handling and request deduping. However, the fine-grained cache querying is not yet available. There is no indication if or when that might become available. Back to Vuex/Pinia for now...
- Vue@2 is stuck in a by-gone era and will never enable this.

### Reference:

- [8 free to use GraphQL APIs](https://www.apollographql.com/blog/community/backend/8-free-to-use-graphql-apis-for-your-projects-and-demos/)
- [Thinking in Graphs](https://graphql.org/learn/thinking-in-graphs/)
- [The concepts of GraphQL](https://www.apollographql.com/blog/graphql/basics/the-concepts-of-graphql/)
- [Apollo Client: request caching](https://www.apollographql.com/docs/react/data/queries#supported-fetch-policies)
- [Apollo Client: cache querying](https://www.apollographql.com/docs/react/caching/overview)
- [Vue Apollo Client](https://www.apollographql.com/blog/frontend/getting-started-with-vue-apollo/) / [Getting Started with Vue Apollo](https://www.apollographql.com/blog/frontend/getting-started-with-vue-apollo/)
- [GraphQL Codegen](https://the-guild.dev/graphql/codegen)
- [GraphQL CodeGen: Death by 1000 maybes](https://www.reddit.com/r/graphql/comments/racbjh/graphqlcodegen_death_by_1000_maybes/)

Troubleshooting:

- [How to fix unknown fragments types in GraphQL codegen](https://ifedyukin.ru/blog/all/how-to-fix-unknown-fragments-types-in-graphql-codegen/)
- [How to apply automated type generation on local fields](https://stackoverflow.com/questions/53839749/apollo-clientcodegen-typescript-with-client-query-fields)

Learn More:

- [https://graphql.org/](https://graphql.org/)
- [https://the-guild.dev/blog](https://the-guild.dev/blog)
- [https://www.apollographql.com/tutorials/browse](https://www.apollographql.com/tutorials/browse)

---

[^1]: Single Page Application (SPA): Is a web application or website that interacts with the user by dynamically rewriting the current web page with new data from the web server, instead of the default method of a web browser loading entire new pages. The goal is faster transitions that make the website feel more like a native app. [wikipedia](https://en.wikipedia.org/wiki/Single-page_application)
