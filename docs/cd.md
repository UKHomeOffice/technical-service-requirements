## Continuous Deployment

### As a service, I should:

- Be deployed as an isolated entity
- Not require other versions to be deployed with me
- Expose a readiness probe that meets my requirements (i.e. the versioned services I need are there hence I am ready)
- Expose a liveness probe to check and monitor my health once deployed
- Expose useful metrics about myself
- Be able to recover from failures of dependent services once I am deployed
- Cleanly / gracefully close threads / sockets if I am told to stop running
- Be able to run multiple instances of me
- Be able to run multiple versions of me in parallel
- Be able to deal with schema migrations as part of my deployment natively
