---
title: Webinars/2023/CircleCI Config Policies and recent security features in CircleCI
---
CircleCI Config Policies and recent security features in CircleCI
===

## Config Policies

- also has human readable error messages
- enable freedom to write, guard rails written by platform engineer /
  DevOps
- policies can only be configured by org admin
- can have soft and hard fail
    - hard fails
    - soft just logs to be audited later
- new rules are not enabled by default
- eval page: https://app.circleci.com/policy-playground
- CLI has policy stuff as well, managing and also validating locally
- can be pushed and validated inside pipeline utilizing repo
- currently only scale plan and public preview currently


### in a nutshell

- uses Open Policy Agent engine
- boolean decission if can run or not
- everything you can configure can have a policy


### examples

- docker image enforcement
- resource class optimization
- restrict context by project


## Learnings

- context can be scoped to user group, which can also be used as
  failsafe for jobs that should not be runnable by all users
- IAM roles used with web-identity-role can also be limited to users,
  not only project


## Questions and Conclusions


### Why do i need at least one context assigned to utilze OIDC

- OIDC and context implementation is currently tightly connected, which
  requires a context to be present


### Set context owners via API

- Currently not possible, but taking to product team
