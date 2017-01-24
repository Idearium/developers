# Idearium Node.js Developer Style Guide

This is an Idearium style guide for Node.js developers.

The purpose of a style guide, is so that all developers write the same code. Consistent, readable code across large code bases is important. Ideally, you shouldn't be able to tell the difference between different authors of the same code base.

- [nodejs.md](./nodejs.md) is the actual style guide.
- [.eslintrc](./.eslintrc) can be used for Node.js linting in your editor.

## Languages

Specific languages are covered as required.

- [Node.js](./nodejs.md)

## Linting

We use [eslint](http://eslint.org/) for linting Node.js code. There is an Atom Editor plugin called [linter-eslint](https://atom.io/packages/linter-eslint) to use the `.eslintrc` file.

If you're creating a new project, make sure to copy the [.eslintrc](./.eslintrc) across to the repository.

### Requirements

Our eslint config relies on an a 3rd party config `eslint-config-airbnb`.
To install it you need to run a command inside your vm:

```shell
# @ /vagrant/
$ (
        export PKG=eslint-config-airbnb;
        c npm app info "$PKG@latest" peerDependencies --json | command sed 's/[\{\},]//g ; s/: /@/g' | xargs c npm app install --save-dev "$PKG@latest"
  )
```
