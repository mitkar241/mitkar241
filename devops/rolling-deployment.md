# rolling deployment
---
## What are rolling deployments?
---
Rolling deployments are a strategy to deploy a new version of an application without causing downtime. They work by creating a single instance of the new version of an application, then shutting off one instance of the old version until all instances have been upgraded.

For a concrete example, let's re-visit our good friend from the rest of the Academy Devops series - the MERN app

Let's say your app has enough traffic that users will notice (and mind) if it goes down for a little while. How would you push a new version of the your application without causing downtime?

A common way is with a rolling deployment. The high level algorithm for rolling deployments looks like this:

- Create an instance of the new version of the backend.
- Wait until new copy is up ("healthy")
- Delete an instance of the old version of the backend.
- If any instances of the old version still exist, go back to step 1.

In our MERN example, we'd initially see 3 instances of the initial version, and 1 instance of the new version, and we'd repeat the process until we had 3 instances of the new version and 1 instance of the initial version

#### Benefits of rolling deployments

Well supported: Rolling deployments are relatively straightforward to implement in most cases. They are natively supported in several orchestrators including kubernetes and Amazon's Elastic Beanstalk.

No huge bursts: One key benefit of rolling deployments is that they reduce the number of services running - a naive blue/green deployment might start 6 API servers at once, double the regular production load. It's not an uncommon occurance for databases to hit concurrent connection limits if the number of services doubles in a short period of time.

Easily reverted: Another benefit of rolling deployments is that it's easy to roll them back if something goes wrong. If, in the course of the upgrade, you notice problems - it's usually possible to "reverse" the rolling deployment to start removing the new version of the app and re-starting the old version.

#### Downsides of rolling deployments

Speed: It can be slow to run the algorithm specified above - some deployments might have thousands of copies of a service running, so a rolling deployment might take over an hour if done one at a time. This can be mitigated by increasing the number of services being turned on / shut off at a time (sometimes called "burst limit")

API compatibility: This is the biggest drawback of rolling deployments. Say you've added the endpoint /api/hello to v2 of your backend, and consume /api/hello in v2 of your frontend. It's possible that a user would have their request sent to v2 of your frontend, but v1 of your backend (because there are still copies of the latter running during the deployment.) This can be mitigated with more complicated routing techniques, but it's generally better to make APIs be backwards compatible whenever possible.

## Closing thoughts
---
Rolling deployments are relatively simple to understand, and generally well supported by orchestrators. If your users mind when you have downtime, it's an excellent first step to start deploying using a rolling update strategy.

The key programming consideration is to ensure that services can consume both the old version and the new version of other services' APIs. If this contract is violated, your users might still see errors during the deployment.
