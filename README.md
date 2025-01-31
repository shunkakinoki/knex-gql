# knex-graphql

[experimental] A GraphQL Query Builder using Knex.js

# Why

Creating a GraphQL service with a Relational Database is a hard thing. We should take care of:

- Performance. N+1 problem will happen if you don't use Dataloader
- Pagination. Dataloader pattern is hard to implement pagination without a hacky `union` or window functions.
- Security. Keeping private fields needs much more work.
- Code Reusability. GraphQL frameworks provides the Middleware function, but it is often not enough.
- Realtime. Using GraphQL subscritpion is a challenging task.
- Type Safety. How to type GraphQL result without relying on Codegen?

So, why not integrate Knex with GraphQL directly?

# POC

```graphql
type User @table(name: "users") {
  id: ID!
  name: String!
}

input UserInput {
  name: String!
}

type Query {
  user(id: ID! @eq): User! @find
}

type Mutation {
  createUser(input: UserInput!): User! @create
}
```
