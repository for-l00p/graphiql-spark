# GraphiQL Spark

GraphiQL Spark exists to demo a GraphQL schema without any GraphQL endpoint.

It allows you to run queries or mutations completely client side a.k.a serverless!
In addition the query/mutation response is rendered once GraphiQL is mounted, which makes it ideal for blog posts.

## How is it different to GraphiQL?

Not by much. GraphiQL Spark is thin convinience layer on top of GraphiQL.

## Benefits

- No Downtime (your static site might work, but the GraphQL endpoint might be down)
- No Server Cost (why pay for demoing a GraphQL concept on your blog?)
- Faster feedback loop (no network request)

## How to use

```js
import React from 'react';
import GraphiQlSpark from 'graphiql-spark';
import 'graphiql/graphiql.css';

// Schema defined in the Schema Definition Language
const typeDefs = `
  type Post {
    title: String
  }

  type Query {
    posts: [Post]
  }
`;

// Client-side resolvers
const resolvers = {
  Query: {
    posts: () => [
      { title: 'Advanced GraphQL Concepts' },
      { title: 'Why I Write CSS in JavaScript' },
    ],
  },
};

// Example query
const query = `query {
  posts {
    title
  }
}
`;

export default function Example() {
  return (
    <div style={{ height: 400, maxWidth: 640 }}>
      <GraphiQlSpark query={query} resolvers={resolvers} typeDefs={typeDefs} />
    </div>
  );
}
```

## FAQ

### Are relations (mutually-recursive resolver) possible?

Yes

### Are Mutations supported?

Yes

### Are Subscriptions supported?

No, but I would welcome a proposal on how this could be done.

### How does it work?

GraphiQL Spark builds a Schema locally in the browser and then directly can invoke the Schema instead of using a Transport Layer like HTTP.

### Can I use it with GraphQL Nexus or other Code-First Schema Generators?

Not yet, but probably makes sense to publish such a version. Ping me if you are interested to help. Ideally it would be a named export, but we make sure non-used dependencies are tree-shaked.

## Inspiration

Once upon a time I was giving a GraphQL beginner workshop using the The Star Wars API example. I wanted that in this example every GraphQL request is not more than a simple HTTP request. My attempt to demo this live failed since the example was built in a way that the production version would include a client side schema.

Once I started working on a new personal blog covering GraphQL concepts I was looking for a way to provide executable examples (instead of pasting text or images). And instead of finishing my blog post I procrastinated and built this tool 😄

## Contributing

```
yarn start # or `npm start`
```

This builds to `/dist` and runs the project in watch mode so any edits you save inside `src` causes a rebuild to `/dist`.

To do a one-off build for production, use `yarn build` or `npm run build`.

### Docs

To run the docs locally (the examples are helpful during development) inside another tab run:

```
cd example
yarn # or `npm i` to install dependencies
yarn start # or `npm start`
```
