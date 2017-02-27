## Security

### As a Service, I should: 

- Follow the [UK Home Office security guidelines for developers](https://github.com/UKHomeOffice/security-guide-for-developers)
- Always use TLS 1.2 encryption to my service and to dependent services (even datastores)
- Use SSO for users and not hold users locally
- Have a way of providing auditable information on myself
- Have authentication / authorization for dependent services where data needs to be protected
- Not have my services or applications run as root.
- Not have the filesystems on my systems as writable, with exception of the specific paths that require this.
