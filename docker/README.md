# Docker

We use Docker to build agile software delivery pipelines to ship new features faster, more securely and with confidence.

All Docker containers are built from base images running [Alpine linux](https://www.alpinelinux.org/) and [s6](http://skarnet.org/software/s6/) process management.

Refer to [docker-alpine](https://github.com/smebberson/docker-alpine) repository for various Docker base images.

## Why we Dockerise our application:

- The development environment is the exact same as production environment. This means, you can deploy and it will "just work", if it works on development.

- Deployment is easy. Just package up your code and deploy it on a server with the same image.

- Easy to test: Using Docker makes our code more testable because we can easily start it on any environment (i.e. CI/CD) and run it.

- Portability: Packaging up our code in Docker images means you can run it wherever you can run Docker - which is pretty much anywhere!

## Multi-process philosophy

We do not believe in the common Docker philosophy of one process per container. We recommend and use a proper init system within our containers. There are many reported problems about using a non-init system as PID 1.

We require the ability to run more than one process in our Docker containers for the purpose of:

- Linux runtime improvements (for example, we replace the inbuilt DNS server with go-dnsmasq).

- Remote log aggregation requiring processes that run, analyse and collect information from log files.

 We use following common services inside Docker containers in most our projects:

 - Nginx:  web server for serving static content. [More information](https://github.com/smebberson/docker-alpine/blob/master/alpine-nginx/README.md) on how to containerize and use Nginx as a Proxy

 - Consul: We use consul for discovering and configuring services in Docker infrastructure. [Read](https://www.consul.io/intro/) for more informartion on consul

 - Logentries linux agent: We use logentries linux aget to acceess Logentries logging infrastructure from application. [More on](https://docs.logentries.com/docs/linux-agent) Logentries agent.

__Note:__ We use __s6__ to allow us to use and manage multiple processes inside Docker container, as mentioned previously.
