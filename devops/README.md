# Idearium Devops

Devops is a core focus at Idearium. Developers using a development workflow that is solid and just works, are happy, productive developers.

Devops is all about how we develop our applications. This document describes our approach to devops. Our devops is achieved through three key projects:

- [Infrastructure common][infrastructurecommon]
- [Idearium cli][ideariumcli]
- [Idearium lib][ideariumlib]

Infrastructure common is used to simulate all of the managed services that we use at runtime. The Idearium cli is how we automate development practices as much as possible. The Idearium lib is library of code that we use to automate often used concepts within our programming.

You should read about each project, as they work hand in hand to enable devops at Idearium.

## Developing projects

We use the following to develop projects:

- [VMware Fusion][vmwarefusion]
- [Infrastructure common][infrastructurecommon]
- [Minikube][minikube]

Infrastructure common provides RabbitMQ, MongoDB and Redis and is run within a VM. It also provides Kubernetes ingress (via Minikube) so that each project can be access locally via domain names.

[infrastructurecommon]: https://github.com/idearium/infrastructure-common
[ideariumlci]: https://github.com/idearium/cli
[ideariumlib]: https://github.com/idearium/idearium-lib
[minikube]: https://github.com/kubernetes/minikube
[vmwarefusion]: https://www.vmware.com/au/products/fusion.html