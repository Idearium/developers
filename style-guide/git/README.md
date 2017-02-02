# Idearium Git Style Guide

This is an Idearium style guide for Git.

The purpose of a style guide, is so that all developers write the same code. Consistent, readable code across large code bases is important. Ideally, you shouldn't be able to tell the difference between different authors of the same code base.

## Branching

All repos should follow a similar branching style to ensure a smooth development process.

There are 2 rules to git branching:

  1. If the user story can deliver benefit to the customer without linking to other user stories, one branch from master should be sufficient.

  2. If the user story must be combined with others before delivering benefit to the customer, one epic (feature) branch, and then subsequent story branches should be used.


```shell
master          # → Never push to this directly, always do a PR.
├── general     # → General branch
└── epic        # → Epic/feature branch
    ├── XX-01   # → Story branch
    ├── XX-02   # → Story branch
    └── XX-03   # → Story branch
```
