# Idearium Developers Stack

This document outlines all of the technology we use so that you can familiarise yourself with it.

## Core tech stack

We've split our core tech stack down into a few different categories:

### DevOps

- Minkube.
- Git.
- Idearium cli.
- Infrastructure common.

### Application services

- Node.js.
- Mongo.
- Express.
- Linz.
- Redis.

### Infrastructure

- Docker.
- RabbitMQ.
- Kubernetes.

### Client-side

- Angular.js.
- Vue.js.
- SaSS/Less.
- jQuery.

## DevOps

DevOps is super important. The more happy the developer, the better her code.

### Idearium cli

We have our own cli that we use and bake into all of our processes. It underpins our philosophy to development.

### Infrastructure common

All of our projects depend on a similar architecture. In production, we also use as many managed services as we can. Infrastructure common is the managed services, but for production. We also use it to coordinate depedency installation for all of our projects.

### Git

We use [Git][git] for versioning and [GitHub][github] for repository hosting.

## Application services

These drive our core application services, or back ends.

### Node.js

We use [Node.js][nodejs] as our application server.

### Nginx

We use [Nginx][nginx] as our primary web server. We use it to serve static files, and to proxy to our application servers.

### Caddy

[Caddy][caddy] is an alternative web server that we use. It serves static files, and proxies to our application servers.

### Mongo

[MongoDB][mongodb] is our choice of primary database, but we do use others were appropriate.

### Express

[Express][express] is our choice of frameworks for our Node.js applications.

### Linz

[Linz][linz] is our home-grown Node.js framework, built on top of Express. We use it to rapidly create Administration interfaces.

### Redis

We use [Redis][redis] as our caching server (Node.js), and back-end for job queues services.

## Infrastructure

Infrastructure is the tech we use to power our applications.

### Docker

We use [Docker][docker] as our microservices runtime for all environments including development, beta, staging, production.

### Kubernetes

We use [Kubernetes][kubernetes] as our microservices orchestration engine.

### RabbitMQ

[RabbitMQ][rabbitmq] is our choice of messaging infrastructure. We use it to bring together our loosely coupled microservices architecture.

## Client-side

Everything browser side.

### AngularJS

We use [AngluarJS][angularjs] as our primary choice of client-side JavaScript framework.

### Vue.js

[Vue.js][vuejs] is our second choice of client-side JavaScript framework. It is also likely to become our primary in the near future.

### jQuery

We use [jQuery][jquery] for DOM manipulation, but nothing else. It shouldn't be used in place of a client-side framework.

### Bootstrap

We use [Bootstrap][bootstrap] as our CSS/HTML framework.

[nodejs]: https://nodejs.org/en/
[docker]: https://www.docker.com/
[mongodb]: https://www.mongodb.com/
[redis]: https://redis.io/
[rabbitmq]: https://www.rabbitmq.com/
[kubernetes]: https://kubernetes.io/
[linz]: https://github.com/linzjs/linz
[express]: http://expressjs.com/
[vagrant]: https://www.vagrantup.com/
[gulp]: http://gulpjs.com/
[git]: https://git-scm.com/
[github]: https://github.com/
[angularjs]: https://angularjs.org/
[vuejs]: https://vuejs.org/
[sass]: http://sass-lang.com/
[less]: http://lesscss.org/
[jquery]: https://jquery.com/
[bootstrap]: https://getbootstrap.com/
[nginx]: https://www.nginx.com/
[caddy]: https://caddyserver.com/
