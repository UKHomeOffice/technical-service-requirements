## Service Discovery

### As a service, I should:

* Have a way of discovering my own dependencies
* Wait for my dependencies to be available before then consuming them
* Not fail if my dependency fails or disappears, but wait for it to return 

### How

Typically this would be achieved through the readiness check on your containers. i.e. Test whether the container's external dependencies are available and fail the check if not. That way, traffic will not be routed to your pod when it cannot reach its dependencies. As soon as the dependencies are available the check will pass and traffic will be routed through to the pod once more.

**Note:** A missing external dependency should not cause a liveness check to fail as the container itself is not at fault.
