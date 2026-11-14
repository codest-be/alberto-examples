# Alberto examples

Example applications for [Alberto](https://github.com/codest-be/alberto), the DCB event store for
.NET. They consume Alberto from nuget.org exactly as your application would.

| Path | What it is |
|------|------------|
| `apps/Alberto.Orders` | Orders module: vertical slices, EF projections, GraphQL (HotChocolate) |
| `apps/Alberto.Payments` | Payments module, same shape, served by the Orders API host |
| `apps/Alberto.AppHost` | Aspire host: PostgreSQL, migrations, the Orders API, K6 load tests |
| `tests/Alberto.Examples.Tests` | Decider and projection specifications (`Alberto.Testing`), GraphQL schema snapshot |
| `tests/Alberto.Orders.LoadTests` | K6 load tests (TypeScript) |
| `docs/vertical-slices.md` | How the modules are sliced, and why slices share nothing but the event log |

```bash
dotnet run --project apps/Alberto.AppHost      # PostgreSQL + migrations + Orders API
dotnet test                                     # Decider/projection specs and schema snapshot
```

The decider tests under `tests/Alberto.Examples.Tests` are the reference for how a slice's tests
should read with `Spec.For(evolver).Given(...).When(...).Then...`.

To accept an intended GraphQL schema change, run the tests with `REWRITE_SNAPSHOT=1` and commit
the rewritten `Snapshots/schema.graphql`.

Split out of the Alberto repository at codest-be/alberto@d130c69.
