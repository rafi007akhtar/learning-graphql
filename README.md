# Learning GraphQL

As I'm learning the basics of GraphQL from https://www.howtographql.com/, I will store my notes here.

## Fundamentals

- GraphQL enables _declarative_ data fetching, where the client can specify exactly what data it needs from an API.
- It exposes a **single endpoint** that responds to queries, instead of multiple endpoints returning fixed data.
- The **n + 1 problem**: when we get a list of items from an endpoint, but to get the required information for each of those items, we need to hit a dedicated endpoint, so this way, we need to hit one _extra_ endpoint for each of the items obtained (essentially, we are _underfetching_ in the beginning).
- GraphQL uses _resolver_ functions to collect the data requested by the client, and those provides insights on the bottlenecks in your system.
- The GraphQL **Schema** serves a _contract_ between the client and the server, allowiing both teams to work completely independent of each other.
- The **Schema Definition Language** (SDL) is the syntax for writing the schema.

### Examples of types

```graphql
# a Post type with a title and an author attributes
type Post {
  title: String! # the ! means it's a mandatory field
  author: Person! # the Person is another type, so this means each Post can have a single Person as its author
}
```

```graphql
# a Person type with name, age and posts as attributes
type Person {
  name: String!
  age: number!
  posts: [Post!]! # this means an array of posts, so a Person can author many posts in this case
}
```

### Examples of fetching data

This corresponds to GET calls with REST APIs, where data is just fetched.

To get name from `allPersons`:

```graphql
allPersons {
    name
}
```

To get name and age:

```graphql
allPersons {
    name
    age
}
```

Same as above, but for the last two people stored in the database (using query params):

```graphql
allPersons(last: 2) {
    name
    age
}
```

### Examples of mutations

This is analogous to POST calls with REST API, where data might need changing. Mutations can be done for creating new data, updating existing data, or deleting existing data. Mutations always start with the `mutation` keyword, followed by a root field.

To create a new person with some name and age, and then query for the name and age after getting the data created:

```graphql
mutation {
  createPerson(name: "Rafi", age: 29) {
    # createPerson is the root field
    name
    age
  }
}
```

GraphQL automatically creates unique ids for their types, if specified in the schema (I think). So now, I want to extend the `Person` type with an id and get back the same when a new person is created.

Change in the type:

```graphql
Person {
    id: ID! # NOTE: this line
    name: String!
    age: number!
    post: [Post!]!
}
```

Change in the mutation:

```graphql
mutation {
  createPerson(name: "Rafi", age: 29) {
    id
  }
}
```
