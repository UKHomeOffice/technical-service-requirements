## Continuous Integration

### As a service, I should:

- Make sure I stub ALL dependent services
- Use in-memory datastores for unit/integration tests if you have to test with data
- Make sure I follow the [testing pyramid](https://googletesting.blogspot.co.uk/2015/04/just-say-no-to-more-end-to-end-tests.html)
- Make sure all services have independent lifecycles from each other i.e. separately versioned (they may depend on specific versions of each other but not rely on being coupled)
- Make sure I can iterate on a service without breaking services that depend on me
- Make sure I take ownership of schema migration and test this as an integration test
- Make sure I do BDD at the source of that service and not across multiple services (leave that for light end-to-ends)
- Use protective branches and not be able to merge into master if any of my tests fail
- Need a peer review of my code before my PR can be merged
- Make sure the person working on code for me can not merge in their own code
- Only perform unit tests on branch pushes
- Do integration and acceptance tests on PR requests before they are merged
- Deploy a merge to master into an environment (whether ephemeral or static) to perform a light end-to-end, not repeating the above steps
- Perform quick end-to-end tests that are there to just validate that things work together as expected, (no need to repeat unit / acceptance tests already done)
