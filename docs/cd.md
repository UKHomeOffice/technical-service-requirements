## Continuous Deployment

### As a service, i should:

- Be able to be deployed as an isolated entity
- Not require other versions to be deployed with me
- Expose a readiness probe that meets my requirements i.e. (the versioned services i need are there hence i am ready)
- Have a liveness probe to check and monitor my health once deployed
- Be able to recover from failures of dependent services once i am deployed
- Cleanly / gracefully close threads / sockets if i am told to stop running
- Be able to run multiple of me
- Be able to run multiple versions of me in parallel
- Be able to deal with schema migrations as part of my deployment natively
- Expose useful metrics about myself
