# Idearium Git Developer Style Guide

This is an Idearium style guide for Git.

The purpose of a style guide, is so that all developers write the same code. Consistent, readable code across large code bases is important. Ideally, you shouldn't be able to tell the difference between different authors of the same code base.

## Branching

All repos should follow a similar branching style to ensure a smooth development process.

There are 2 main types of branches:

- *General*, which provides a benefit to all contributors.
- *Epic*, which should include the Jira epic name. *Feature* branches should then be added to this and use the Jira task ID.

```shell
master          # → Never push to this directly, always do a PR.
├── general     # → General branch
└── epic        # → Epic branch
    ├── XX-01   # → Feature/story branch
    ├── XX-02   # → Feature/story branch
    └── XX-03   # → Feature/story branch
```
