# Kubernetes

We use Kubernetes as our orchestration engine to run our microservices.

## Kubernetes conventions

These are the conventions we've developed and used within Kubernetes.

### Manifests

Kubernetes has two modes of operation:

- Imperative commands
- Declarative object configuration

We solely use declarative object configuration. This has the advantage of being able to version control your Kubernetes spec. This is important so that environments can easily be recreated exactly as they were previously.

All of our manifests are seperated by environment, and stored in a projects `manifests` directory (i.e. `manifests/local` for the local environment and `manifests/production` for the production environment).

#### Templates

The Idearium cli, responsible for applying Kubernetes manifests to a cluster, has the capability to work with template variables. If you create a file ending in `.yaml.tmpl` the cli will know to parse the file through Mustache and generate a `.yaml` file.

All files are stored in `manifests/location/.combined/`. Files ending in `.yaml` are copied across without being run through Mustache. The files store in `.combined` are passed to Kubernetes.

### Ingress

We use Kubernetes ingress to ensure multiple projects can be run from one local Kubernetes cluster (via Minikube). We don't use the Minikube ingress addon, but use our own custom Ingress controller.

### Namespace

Each project has it's own namespace. Kubernetes namespaces provides you with isolation of Kubernetes objects running on a cluster. Our namespaces are defined with the following convetion `{organisation}-{project}-{environment}`. The only Kubernetes objects we run in the `default` namespace is our ingress controllers.

### Labels

Kubernetes using labels and selectors, to determine what runs where, and how to route requests from a service to a deployment, or a pod. We use the following setup for our labels:

- `SVC` is the name we use to define a service (conceptually similar to services in Docker Compose).
- `SVC=app` where `app` is the name of a Kubernetes location.

## Kubernetes gotchas

Everything has quirks, and Kubernetes has a few too. Here are some things you should know about Kubernetes.

### kubectrl config

`kubectrl` can be configured to work in multiple contexts. You can see the current context with `kubectrl config view`.

When you use `c kc context set` to set `kubectrl` up for a specific project, it does it globally against the `kubectrl` command. Be aware of that when jumping from project to project.

Alternatively, always use `c kc cmd` (i.e. `c kc cmd get all`) to execute `kubectl` commands. `c kc cmd` ensures the commands are always run with the Kubernetes context and namespace of the project you're running the command from.