# Learning GraphQL

As I'm learning the basics of GraphQL from https://www.howtographql.com/, I will store my notes here.

## Fundamentals

- GraphQL enables _declarative_ data fetching, where the client can specify exactly what data it needs from an API.
- It exposes a **single endpoint** that responds to queries, instead of multiple endpoints returning fixed data.
- The **n + 1 problem**: when we get a list of items from an endpoint, but to get the required information for each of those items, we need to hit a dedicated endpoint, so this way, we need to hit one _extra_ endpoint for each of the items obtained (essentially, we are _underfetching_ in the beginning).
- GraphQL uses _resolver_ functions to collect the data requested by the client, and those provides insights on the bottlenecks in your system.
- The GraphQL **Schema** serves a _contract_ between the client and the server, allowiing both teams to work completely independent of each other.
