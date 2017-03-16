# Docker

We use Docker to build agile software delivery pipelines to ship new features faster, more securely and with confidence.

All docker containers are built from base images running [Alpine linux](https://www.alpinelinux.org/) and [s6](http://skarnet.org/software/s6/) process management.

Refer to [docker-alpine](https://github.com/smebberson/docker-alpine) repository for various docker base images.

### Why we dockerise our application:

- Consistent development environments for entire team. All developers use the same OS, same system libraries, same language runtime for each project, no matter what host OS each team member are using.

- The development environment is the exact same as production environment. This means, you can deploy and it will "just work", if it works on development.

- Deployment is easy. Just package up your code and deploy it on a server with the same image.

### Docker philosophy

 We do not believe in one process per container philosophy of docker, as we require multiple processes to co exist in container for our application.

 We use following common services together with Node.js inside docker containers in most our projects:

 - Nginx:  web server for serving static content. [More information] (https://www.digitalocean.com/community/tutorials/docker-explained-how-to-containerize-and-use-nginx-as-a-proxy) on how to containerize and use Nginx as a Proxy

 - Consul: We use consul for discovering and configuring services in docker infrastructure. [Read] (https://www.consul.io/intro/) for more informartion on consul

 - Logentries linux agent: We use logentries linux aget to acceess Logentries logging infrastructure from application. [More on] (https://docs.logentries.com/docs/linux-agent) Logentries agent.

__Note:__ We use __s6__ to allow us to use and manage multiple processes inside docker container, as mentioned previously.
