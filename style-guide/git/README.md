# Idearium Git Style Guide

This is an Idearium style guide for Git.

The purpose of a style guide, is so that all developers write the same code. Consistent, readable code across large code bases is important. Ideally, you shouldn't be able to tell the difference between different authors of the same code base.

## Branching

All repos should follow a similar branching style to ensure a smooth development process.

There are 2 rules to git branch naming:

  1. If the user story can deliver benefit to the customer without linking to other user stories, the story ID should be used.

  2. If the user story must be combined with others before delivering benefit to the customer, use a descriptive name.


```shell
master                 # → Never push to this directly, always do a PR.
├── XX-01              # → User story ID.
└── sso-integration    # → Describes what the branch intends to do.
```

## Branch protection

All repos should be setup with GitHub branch protection. This creates a process for merging from a branch into master. To setup branch protection, you should follow [this guide](https://help.github.com/articles/about-protected-branches/).

We use the following setup for branches:

- Default branch: `master`
- Protected branches: `master`
  - Require pull request reviews before merging: `checked`
    - Include administrators: `unchecked`
  - Require status checks to pass before merging: `checked`
    - Include administrators: `unchecked`
    - Require branches to be up to date before merging: `checked`
  - Restrict who can push to this branch: `unchecked`
