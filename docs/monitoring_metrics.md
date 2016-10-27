## Monitoring and Metrics

### Pre-Reqs

There are some expectations around the monitoring, that is to understand concepts such as liveness and readiness

* Liveness - Is the current running state and health of the application service
* Readiness - This is when the service is ready to be consumed. An example is performing some schema migrations or waiting for dependent services to be ready before your service can be ready. We wouldn't want the service to be consumed until it is ready to be so.


### As a service we expect there to be:

* A `/metrics` endpoint for your service to expose all necessary metrics
  Used by `Prometheus` for monitoring and alerting
* A `/healthz` endpoint for the liveness Probe
  Used by `Kubernetes` for cluster maintenance; should respond with the `200` success status, otherwise the node will be restarted
* A `/readiness` endpoint for the readiness probe
  Used by `Kubernetes` for cluster maintenance; should respond with the `200` success status, otherwise the node will be taken out of the active pool and will not receive further [external] requests until it is ready again (resumes responding with `200` status)
