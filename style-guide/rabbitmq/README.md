# Idearium RabbitMQ Style Guide

This is a guide for consistently using RabbitMQ.

It is licensed under the [CC BY-SA 3.0][cc] license. You are encouraged to fork this repository and make adjustments according to your preferences.

[cc]: http://creativecommons.org/licenses/by-sa/3.0/
![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## Microservices

We primarily use RabbitMQ to provide integration between our loosely coupled microservices. We also use RabbitMQ to distribute time consuming tasks amongst multiple workers.

## Exchanges, queues and routing keys

Use the following as guidelines for naming your exchanges, queues and routing keys.

### Exchange

There are 3 types of exchanges:

- **fanout**, which doesn't provide you much flexibility. It sends one messages to all consumers that are listening.
- **direct** which routes messages to consumers whose queue _binding key_ exactly matches the _routing key_ of the message.
- **topic** which is the most complex, but also the most flexible. It is similar to a direct exchange but allows more flexible routing by using wildcards.

We exclusively use topic exchanges for their flexibility.

Choose one of the following to name your exchange:

- `create`
- `created`
- `update`
- `updated`
- `delete`
- `deleted`
- `success`
- `fail`

Note the use of tense to separate requests from notifications. You should use present tense (i.e. `create`) when making a request for something to be completed. You should use past tense (i.e. `created`) to announce that something has happened.

`success` and `fail` exchanges can be used when announcing successful, or failed processes.

### Queues

Queues are used to store messages, while they're on their way to a consumer.

Queue names are important to determine which messages your consumers are capable of working on.

- To have your consumers receive messages with the same routing key in a round-robin fashion) use a common name.
- To have your consumers receive messages with the same routing key in in a fanout fashion, use a unique name.

We almost always use a unique name. Use the following convention to name your queues `{project}.{container}.{model|process}.{file-name}`, which provides a unique queue name.

Within our stand setup, unique names only become common, if there are more than one container of the same type (i.e. multiple `app` containers running). However, as the consumers have the same code, this doesn't present a problem as each consumer will receive a message in a round-robin fashion.

### Routing keys

The naming convention for routing keys is important because it allows you to create consumers that can listen to different types of messages coming through RabbitMQ.

Use the following convention to name your queues `{project}.{container}.{model|process}[.{process}]`.

For example:

- `project.app.user` is `{project}.{container}.{model}`.
- `project.api.user.activated` is `{project}.{container}.{model}.{process}`.
- `project.api.member` is `{project}.{container}.{model}`.
- `project.api.analtyics-consolidation` is `{project}.{container}.{process}`.
