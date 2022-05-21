# blue/green deployment
---
## What is a blue/green deployment?
---
Blue/green deployments are a strategy to deploy a new version of an application. They work by starting an entirely new instance of the application, and then routing traffic over to it.

Let's again consider our friendly stack from the rest of the Academy Deployments series, the MERN stack:

Here, we have three types of microservices:

- The Node.js backend - handles requests for objects.
- The React frontend - serves renders HTML and javascript.
- MongoDB - a persistent database that holds data.

## Shared resources and cluster resources
---
To set up a blue/green deployment, teams need to disambiguate which services will be consistently deployed, and which services will be shared across versions of the application.

A database server would be a shared resource. Multiple versions of the app would connect to the server at the same time, and a standard deployment would generally not upgrade or modify the database.

In our MERN example, all of the other services are cluster resources - new versions of them would be deployed on every prod push.

## "Blue" and "Green"
---
Blue/green deployments are so-called because they maintain two distinct clusters, one named "blue" and one named "green" out of convention.

If the current version of the application is deployed to "blue", we would deploy the new version to "green" and use it as a sort of staging environment to ensure that the new version of the app works correctly.

After we're confident that the new version of the software works correctly, we would move over production load from "blue" to "green", and then repeat the cycle in the opposite direction.

## Benefits and drawbacks of blue/green deployments
---
On the benefits side - blue/green deployments are conceptually very easy to understand. To set them up, one must simply create two identical production environments and send requests either to one or the other, as the deployment progresses.

They are also quite powerful - longer running tasks like downloads can continue running in the "old version" of the application after traffic is switched over to the new version.

Additionally, blue/green deployments can be extended to many different workflows, which we'll discuss further down in this post.

There are a few notable drawbacks to blue/green deployments. It's difficult to deploy a "hot fix" quickly (for example, to revert a change) because the old cluster might be running some longer running tasks and unavailable to switch to.

It's also finicky to transfer load between the clusters - if resources scale automatically and load is transferred all at once, the new cluster might not have enough resources allocated to serve the surge of requests.

Finally, if one cluster modifies a shared service (like adding a column to a table in the database), it may affect the other cluster despite not being the "live" one.

## Common additions to blue/green deployments
---
Blue/green deployments are very extensible by their nature. Many teams set up more advanced workflows around the core blue/green idea to improve stability or deployment velocity.

#### Rainbow deployments

Instead of only having two clusters, some teams keep an arbitrary number of clusters (blue/green/red/yellow/...) This is often useful when you have very long running jobs (map reduce, web scraping, video encoding, etc) that cannot be easily transferred across clusters. In a rainbow deployment, old clusters would only be shut off after all of their long-running jobs were done processing.

#### Acceptance tests

Some teams rely heavily on manual QA and don't use continuous deployment. They are often building desktop or mobile apps which need to be published on longer release cycles.

If example.com is being routed to the "blue cluster" (meaning that the blue cluster is the "live one"), it would be relatively simple to deploy a new version of the application to the green cluster, and point new.example.com to the green cluster.

With this setup, the new version of the app could be tested against the production database in the very environment which will soon become production. Such tests are usually called "acceptance tests", because QA and product stakeholders can choose to "accept" the developer team's latest release.

#### Canary deployments

If the new version of your app contains subjective changes (such as editing the UI), it might be ill-advised to push them to all users all at once. The changes may break users' workflows and need to be modified or rolled back in response to user feedback.

In the context of blue/green deployments, a "canary deployment" would be to route around 5% of your users at random to the new cluster, and check that those users do not have negative feedback. If not, the rest of the users can also be switched over to the new cluster, and the cycle can repeat.

## Conclusion
--
Blue/green deployments are a powerful and extensible deployment strategy that works well with teams that are deploying a few times per day. The strategy only starts being problematic in continuous deployment scenarios where there are many services being deployed many times per day.
