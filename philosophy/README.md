# Idearium Development Philosophy

Every good dev-shop has their own approach to development. Overtime, these ideas gel together to form a philosophy on how to go about programming.

We have our own too; and this is it.

## Environment parity

The closer you can get your environments, the better off you'll be.

Especially, you code should NEVER have an `if (process.env.NODE_ENV === 'whatever')` statement. If it does, you haven't thought about it enough (see _Configuration_ below).

Your default environment should always be local too. This saves any local disasters when you development environment has accidently connected to a production database.

## Gitops

If you can store it in Git, you should. Seriously, store as much in Git as possible. If environment variables are a key part of your workflow, then they should be stored in Git too.

## Configuration

Use environment variables and configuration to change settings between environments. This allows you to connect to different databases on development, than you do on production, all without changing any of the connection code.

## Managed services

If someone else can manage uptime, scale and back ups for you, then pay someone else to do it. Managing scale, data backups and high availability is difficult.