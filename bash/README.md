# Bash usage guide

This is a mix between a usage guide and a style guide, it relates to both Bash shell scripts and POSIX shell scripts.

## Bash and POSIX

Idearium typically has two environments in which different shell script interpreters should be used. Bash should be reserved to the Vagrant VM environments, and POSIX shell scripts used in all other environments, for example, our Docker containers.

## File naming

Shell scripts should end with the `.sh` extension. It is okay to have a symlink to the shell script within the `/usr/local/bin` directory that doesn't contain the `.sh` extension.

## Variable naming

Variables within shell scripts should be all uppercase and words separated with underscores (`_`).

_Right:_

`OUTPUT_DATA="value"`

_Wrong:_

`outputData="value"`

_Wrong:_

`output_Data="value"`

## Command substitution

Shell scripts can use the expansion of the standard output of one command in the command line for a second command. This is called command substitution. Prefer the `$()` syntax over the back tick syntax.

_Right:_

`ls -l $(cat list)`

_Right:_

`echo "$(expr $(date +%Y) + 1)"`

_Wrong:_

``ls -l `cat list` ``

## If statements

The following are just short snippets and a quick guide demonstrating how Idearium developers should structure if statements.

However thoughtbot's blog post [_The Unix Shell's Humble If_](https://robots.thoughtbot.com/the-unix-shells-humble-if) is a must read for mastering `if` statements in shell script.

### Checking if a variable exists

This `if` statement will return `true` if the length of the specific string is 0.

```bash
if [ -z "$VAR_NAME" ]; then
    printf "somevalue" > /var/run/s6/container_environment/VAR_NAME
fi
```

### Checking string equality

This `if` statement will return `true` if both strings are equal.

```bash
if [ "A" = "$VAR_NAME" ]; then
    # do something
fi
```
