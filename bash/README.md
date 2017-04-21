# Bash usage guide

This is a mix between a usage guide and a style guide, it relates to both Bash shell scripts and POSIX shell scripts.

## Bash and POSIX

Idearium typically has two environments in which different shell script interpreters should be used. Bash should be reserved to the Vagrant VM environments, and POSIX shell scripts used in all other environments, for example, our Docker containers.

## File naming

All shell scripts should end with the `.sh` extension. It is okay to have a symlink to the shell script within the `/usr/local/bin` directory that doesn't contain the `.sh` extension.
