# autoscaling
---
## What is autoscaling?
---
Autoscaling automates horizontal scaling to ensure that the number of workers is proportional to the load on the system.

Let's see if we can clarify things with a more concrete example.

## Example: A CI system
---
Let's say you were building a CI system (what is CI?) - your users would push code, and you'd have to spin up runners to run tests against that code. You'd see bursts of traffic during your users' business hours, and then significantly less traffic outside of business hours.

For a peak load of 10,000 concurrent CI runs, you'd need a at least 10,000 runners provisioned to avoid queuing. However, at night (off-peak hours) these 10,000 runners would mostly sit idle.

In an ideal world, you'd be able to create or destroy runners as necessary - during peak hours you'd be able to create new ones, and at off-peak hours you'd be able to destroy them. This is the idea for autoscaling.

## Autoscaling in cloud providers
---
It's only possible to create/destroy workers because of cloud providers. At their enormous scale it's possible to offer servers for cheap on small (~1 hour) leases. The most popular technology at the writing of this post is AWS EC2 spot which acts exactly like cloud-hosted VMs, but with large discounts if you provision them for short periods of time.

Another popular technology for autoscaling is Kubernetes' Horizontal Pod Autoscaling, which can be consumed by cloud providers that provide support for it such as Google Kubernetes Engine.

Here are some additional references for autoscaling being provided by cloud providers:

- https://azure.microsoft.com/en-ca/features/autoscale/ (Azure VMs)
- https://docs.microsoft.com/en-us/azure/aks/concepts-scale (Azure containers)
- https://aws.amazon.com/getting-started/hands-on/ec2-auto-scaling-spot-instances/ (AWS VMs)
- https://docs.aws.amazon.com/eks/latest/userguide/horizontal-pod-autoscaler.html (AWS containers)
- https://cloud.google.com/compute/docs/autoscaler (Google VMs)
- https://cloud.google.com/kubernetes-engine/docs/how-to/horizontal-pod-autoscaling (Google containers)

## Autoscaling vs serverless
---
Autoscaling is usually discussed on the timeline of ~1 hour chunks of work. If you took the concept of autoscaling and took it to its limit, you'd get serverless: Define resources that are quickly started, and use them on the timeline of ~100ms.

For example, a webserver might not exist at all until a visitor first requested a page. Instead, it would be spun up specifically for the request, then the page served, and then shut back down.

Serverless is primarily used for services that are somewhat fast to start, and stateless. You wouldn't run something like a CI run within a serverless framework, but you might run something like a webserver or notification service.

Autoscaling is primarily used for services that are slower to start or require state. You'd likely run a CI job within an autoscaled VM or container, not within a serverless container.

As of 2021, the distinction between the models is becoming quite blurred - serverless containers are becoming popular, and they often run for upwards of 1 hour. Within a few years it's likely that serverless and autoscaling will converge into a single unified interface.
