# ephemeral environment
---
## What is an ephemeral environment?
---
Ephemeral environments are temporary deployments that contain a self-contained version of your application, generally for every feature branch. They are often spun up by a Slack bot, or automatically on every commit using hosted DevOps platforms like webapp.io or Heroku.

Temporary environments are overtaking traditional CI platforms as the most valuable DevOps paradigm for technical teams. Because these environments are made on every change, all stakeholders can review a change without needing a development environment.

In general, ephemeral environments lie halfway between the development environments and staging environments - at the extreme, staging is entirely replaced with ephemeral environments in a Continuous Staging workflow.

## Benefits of ephemeral environments
---
The most common reason to adopt an ephemeral environment workflow is that it accelerates the software development lifecycle. Developers can review the results of changes visually, instead of needing to exclusively give feedback on the code change itself.

Additionally, developers can share their work with non-technical collaborators such as designers as easily as sharing a link to the proposed revision.

## Databases in ephemeral environments
---
By their nature, ephemeral environments are temporary and should be isolated from production servers or data. A reviewer should be able to try deleting a resource in a review without fear of affecting production.

In the early implementation of ephemeral environments, it might make sense to connect API servers with read-only permissions to a staging database (e.g., via IAM roles if using AWS) - however, the end goal should be to have a fresh copy of the database for every commit.

An ideal ephemeral database has three attributes:

- Prepopulated - it contains representative, anonymized data - to pass security audits, all Personally-Identifiable Information (PII) must be scrubbed from databases used by ephemeral environments.
- Undoable - If, in the course of a review, data is deleted or modified, it should be easy to reset the database to its original state. This is also crucial for running destructive end-to-end tests that perform actions like registration and account deletion.
- Migrated -  The database uses the schema currently used in production, and has proposed migrations run against it: One of the most common classes of problems uncovered by ephemeral environments are broken or non-performant database migrations.

## Ephemeral environment lifecycle
---
One of the hardest problems to solve when implementing Ephemeral Environments is considering when to create/destroy them.

A classic approach is to tie the lifecycle to the life of a pull request or merge request. When the merge request is first opened, an environment is provisioned, and when the merge request is closed, the environment is cleaned up.

The biggest factor to consider here is cost: If each ephemeral environment costs 10% of production spend, and you have 30 open pull requests, you'll be quadrupling your monthly costs to run environments that are mostly unused.

Another approach is to create a ChatOps bot that allows creating a new environment for a specific branch with a small timeout, but this requires waiting for the environment to be provisioned at the time that it's required.

The best approach is to create an ephemeral environment for every commit, and hibernate them the second they are provisioned, then transparently wake them up as they are required. This is the interface you'll see in professionally hosted providers.

## Continuous Staging
---
The simple idea for Continuous Staging is to merge staging, ephemeral environments, and CI pipelines into a single unified devops workflow.

As your ephemeral environments become more powerful and easier to create, they approach and overtake many aspects of traditional Continuous Integration / Continuous Deployment pipelines.

For example, an ephemeral environment which starts a webserver for every commit could just as easily start a container that runs visual tests against that webserver, or deploy the image used by the webserver.

At its logical conclusion, this concept becomes Continuous Staging, in which CI/CD is merged with ephemeral environments to form a unified CI/CD and review process for every commit.

## Getting started with Ephemeral Environments
---
Ephemeral environments can be set up with 6-12 months of engineering time in your own cloud provider. A Slack bot that responds to `/env-create-for` mybranch with a link that lasts a day is a great place to start.

To avoid having to micromanage starting/stopping environments, it's easiest to use a hosted platform. webapp.io connects to GitHub, and uses hibernation to create a cloud-hosted ephemeral environment for every commit automatically. Try the interactive demo for a more interactive introduction to ephemeral environments.
