## Cloud build standards

### Account Layout

- Separate accounts for separate concerns i.e. CI, Ops, Prod etc. This is because it:
  - decouples usage types into it's own account structure making it a more logical separation due to IAM being global
  - prevents tag names possibly overlapping for common services.
  - allows the audit of that account to be more identiable i.e. changes to prod were expected in the account due to known changes / releases etc.
- Use cross account federation where possible for users
- Have separate audit accounts with restricted policies on that accounts

### Account naming

The name of the AWS account needs to contain useful information, below is a list of things that should be contained within it

| Type | Description | Usage |
| ---- | ------ | ------ |
| Directorate | Directorate Cost number | 1234 |
| Cost Code | Cost code number | 3456789 |
| Portfolio | Portfolio abbreviation | x |
| Project Name | Name of the project | Projectx |
| Env Name | Name of environment for account | test, notprod, prod, ops |

The overall Format would be `DIRECTORATE-COSTCODE_PORTFOLIO-PROJECT-ENV`

### IP allocation

If the account is going to share other services i.e. any internal central service, then the IP allocation will need to be addressed. This is to avoid IP conflicts with other services, that may also be VPN / Peered to the central internal service.

Please discuss this with the team when the account is created.

### General Conventions

If we follow the above, then most of the environment separation will be happening at an account level rather than at a resource level. Where there are multi-tenancy type services i.e. an account with multiple service environments for applications, then the env prefix will be necessary.

Please familiarise yourself with

- Tagging Concepts and what services support / don't support [tagging](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Tags.html)
- [s3 naming restrictions](https://docs.aws.amazon.com/AmazonS3/latest/dev/BucketRestrictions.html)

### Tagging considerations

- Tags can be applied anytime
- Cost allocation reports are only available from the point tags were activated
- After creating a tag [key] for costs, it must be marked activated and added as a cost allocation tag; otherwise it will not be visible in the Cost Explorer

### General Tagging Standards

Below are a list of tagging standards to consider. Not all will be applicable i.e. based on the above shared account concepts (it's hosted in an account with other services), if it's clustered or not.

All of the below should apply however, to all resources where you can.


| Type | Description | Example | Optional |
| ---- | ------ | ------ | ------|
| `TYPE` | Service type | CI, Logging, Monitoring (The service-type
might be elasticsearch but it's overall logging for example)  | Yes |
| `ENV` | Environment | dev, prod, uat, ppd | No |
| `CLUSTER` | Cluster Name | cluster1, cluster2 | Yes |
| `NODE` | Node within the cluster | node1 | Yes |
| `APPSTAGE` | Stage of the application and resources associated | Alpha, Beta, Live | Yes |
| `ACCESS` | Private or Public | private, public | no |
| `PROJECT-SERVICE` | name of the service | projectx, projecty | No |
| `PROJECT-PORTFOLIO` | Name of the portfolio | portfoliox | yes |
| `SERVICE-TYPE` | Type of service | db, webapp, proxy | No |
| `AZ` | availability zone number | 1a, 1b, 1c | No |
| `COST-CODE` | cost code if a shared account | 1234-5678 | yes |
| `REPO` | Repository related to the creation | repo1 | yes |
| `TEAM` | Name of the team if a shared account | team1 | yes |

### Additional Tagging Naming Standards

| Type | Description | Example | Optional |
| ---- | ------ | ------ | ------|
| `RDS-TYPE` | database type | Postgres, mysql, oracle | RDSTYPE: Oracle | No |

### Automation and Cloud Rules

- There **MUST NOT** be manual changes to any resources everything **MUST** be done via code
- Console access **MUST** be locked down to readonly to stop manual changes or changes being made that are not tracked via code
- All code **MUST** be triggered via a CI job and not run manually
- All code **MUST** be tested, linted, and planned
- [Terraform](https://terraform.io)  **SHOULD** be used to manage cloud infrastructure
- Baking images into AMI's using [packer](https://packer.io)  **SHOULD** be used over running configuration management tools post infrastructure build phase [see here for sharing AMI's between accounts](https://github.com/chrisns/packer-encrypt-copy)
- [Cloud config](https://coreos.com/os/docs/latest/cloud-config.html) is preferred where [CoreOS](https://coreos.com) is used to bootstrap the OS
- [cloud-init](https://cloud-init.io) **SHOULD** be used in exchange for baking images as AMI's, though building AMI's **SHOULD** be the preferred choice
- Docker / Containerisation **MUST** be used where possible over native EC2
- **MUST** use multiple [account security structures](https://aws.amazon.com/answers/account-management/aws-multi-account-security-strategy/)
- All accounts **MUST** use the central IAM structure and policies [please read the varied docs on cross account access](https://aws.amazon.com/blogs/security/tag/cross-account-access/)
- All user accounts **MUST** have MFA associated with them
- All users **MUST** rotate their access keys every 90 days
- Projects **SHOULD** change access keys for services used by applications every 90 days
- All user acounts **MUST** assume role and use short lived access keys into the account
- All CI robot accounts **MUST** have locked down policies to restrict to IP's of CI plus detailed policies where possible and multiple robot accounts to reduce risk where possible
- All accounts **MUST** log to central audit
- Firewall management **SHOULD** be as close to the application as possible and not within generic cloud infrastructure (it becomes difficult to manage when there are multiple services sharing)
- All services **MUST** traverse a AWS test account before moving into the AWS production account with validated tests
