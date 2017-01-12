## Continuous Integration

### As a service, I should:

- Make sure I stub ALL dependent services
- Use in-memory datastores for unit/integration tests if you have to test with data
- Make sure I follow the [testing pyramid](https://googletesting.blogspot.co.uk/2015/04/just-say-no-to-more-end-to-end-tests.html)
- Make sure all services have independent lifecycles from each other i.e. separately versioned (they may depend on specific versions of each other but not rely on being coupled)
- Make sure I can iterate on a service without breaking services that depend on me
- Make sure I take ownership of schema migration and test this as an integration test
- Make sure I do BDD at the source of that service and not across multiple services (leave that for smoke tests)
- Use protective branches and allow to merge into master only if tests and status checks pass
- Need a peer review of my code before my PR can be merged
- The code can be merged as long as the tests and status check pass and it is peer reviewed
- Do unit, integration and acceptance tests on PRs before and after they are merged
- Perform automated smoke tests to validate that things work together as expected
- Have clear, concise commit messages conforming to [semantic commit messages](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#), and using the footer to add bug tracker/story ID and/or username(s) if developed in a pair/mob (`git commit --verbose` is useful for multi-line messages)

