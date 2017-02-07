## Containerisation

### As a service:

* I will adhere to [Best practices for writing Dockerfiles](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)
* I will make sure I run as read only, please see https://docs.docker.com/engine/reference/commandline/run/ for the read-only option
* I will make sure my mounted volume has noexec privileges on that volume when it is mounted in
* I will use [Docker/rkt label schema](http://label-schema.org/rc1/) where applicable to define the contents and usage of an image 
* I will inherit from [official Home Office base images](https://github.com/UKHomeOffice/hosting-platform/blob/master/developer-docs/writing_dockerfiles.md) where possible
