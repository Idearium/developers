# Idearium Developer Style Guide

These are Idearium's style guide for developers. They cover both languages, environments and tools.

The purpose of a style guide, is so that all developers write the same code. Consistent, readable code across large code bases is important. Ideally, you shouldn't be able to tell the difference between different authors of the same code base.

## Editors

Enforcing style on code while you're writing complex logic can sometimes be hard. Always use the editor to help ensure you're writing good code.

This repository, where possible, provides editor configurations and linting along with a written style guide.

- [.editorconfig](./.editorconfig) is an editor configuration file. See [editorconfig.org](http://editorconfig.org/) for more information, and download the appropriate plugin for your editor of choice.

### Linting

We use linting where possible to enforce style and correct code (before we attempt to run it). Each language-specific folder should contain the necessary linting files and guides to use them.

## Languages

Specific languages are covered as required.

- [JavaScript (Node.js)](./nodejs/README.md)

## Stack components

These are critical components of our stack.

- [RabbitMQ](./rabbitmq/README.md)

## Tools

These are tools that we use for development, but not necessarily languages.

- [Git](./git/README.md)
