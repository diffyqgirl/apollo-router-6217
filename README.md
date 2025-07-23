repro for https://github.com/apollographql/router/issues/7822

Tested using

- Rover v0.34.1 with federation =2.9.0
- Router v2.4.0

The following three commits show 3 variants of the schema, two fast, one very slow. The key difference is in Type42 (implements Interface4) and how Type42 is federated.

The rest of the schema is present as a scaffolding because the slowdown is not very apparent in a small simple query that just queries Type42 and its interface Interface4.

A note about naming--I have organized it such that Type11, Type12, etc implement Inteface1, Type21, Type22 etc implement Interface2, and so on.

`make supergraph` generates the supergraph, `make run` runs it.

### Case 1: Type42 federated as an entity, runs slowly
This is commit 0add2ff1c2f94b5b415ac80e6bb46acaff5c4fd7.

This took 3.5s in the query planner.

### Case 2: Type42 federated as shareable, runs quickly
This is commit 0802d66028f0ef4bb68c1165122820539b355289

This took 24ms in the query planner.

### Case 3: Type42 in only one subgraph, runs quickly
This is commit 9768b27f32751f3a1d173a55cd69bcce55c63d66

This took 23ms in the query planner.
