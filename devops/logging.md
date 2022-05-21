# Logging
---
## What is Log Aggregation?
---
What is Log Aggregation? It's a way of collecting and tagging application logs from many different services into a single dashboard that can easily be searched.

One of the first systems to be built in an Application Performance Management system is a log aggregation platform.

In most production deployments, there are many related events that emit logs across many services. A single Google search might hit five different services on Google's infrastructure. If you got unexpected search results, that might mean a logic problem in any of the five services.

Log aggregation helps companies like Google diagnose problems in production. They've built a single dashboard where they can map every request to a unique id, and see how individual services are interacting with that request in order to build the response.

This is the essence of a good log aggregation platform: Efficiently collect logs from everywhere that emits them, and make them easily searchable in case of a fault.

## Log aggregation for our MERN app
---
Recall the MERN app from our other webapp.io Academy DevOps series:

Here, we have four components emitting logs:

- The MongoDB instance: As it was configured to
- The Node.js instance: From log statements
- The React frontend: As it serves files to end users
- The user's browser: As exceptions occur (javascript crashes, for example)

If a user told us "the page turned all white and printed an error message", we'd be hard pressed to diagnose the problem with our current stack. The user would need to manually send us the error, and we'd need to match it with relevant logs in our other three services.

Let's look at ELK, a popular open-source log aggregation stack named after its three components: ElasticSearch, Logstash, and Kibana. If we installed it into our MERN app, we'd get three new services:

Not to get too specific to ELK, let's talk about the three general components of a log aggregation system:

#### The log processor (Logstash)

The log processor takes log lines and parses data out of them.

A log line like:
```
1997/01/01 18:03UTC HTTP/1.1 GET /
```
Might be processed into the object:
```
{"date": "01-01-1997 18:03:00", "service": "backend", "msg": "HTTP/1.1 GET /"}
```
The processor will also generally be exposed to the internet so that Javascript on the browser can catch errors and send them to be processed.

#### The data store (Elasticsearch)

The data store is a type of a database, it's significantly more performant for text searching and write speed than a general purpose database.

Elasticsearch allows complex querying. You can, for example, ask for logs between two dates matching a set of filters and containing a particular sentence.

#### The log frontend (Kibana)

The user usually doesn't directly query the data store, instead they interact with a webapp that facilitates querying.

In our example the frontend is Kibana. It lets you search for logs at specific times, matching certain tags, or from certain services.

#### How we'd use ELK to diagnose a production problem

Let's say a user says: "I saw error code 1234567 when I tried to do this."

With ELK set up, all we'd have to do is go to Kibana, and query recent logs for 1234567, that might give us the name of a service: "backend"

Then we could narrow down the time to the five second interval around the error, and filter for log messages emitted by either the backend or the database.

Finally, we'd read those log messages to find the context for the bug.

## Adding authentication to your logging frontend
---
The final piece of the puzzle is ensuring that logs are only visible to administrators. As logs can contain sensitive information (like tokens) it's important that only authenticated users can access them.

To add authentication, all that's required is adding a reverse proxy like nginx in front of the logging frontend, and then using the auth_request mechanism to check that the user is logged in.
```
html.onGET("/auth-request", () => {
  const user = getUser();
  if(!user || !user.isAdmin) {
     return 401;
  }
  return 200;
});
```
And finally, add the following to your reverse proxy configuration:
```
http {
    #...
    server {
    #...
        location /private/ {
            auth_request     /auth;
            auth_request_set $auth_status $upstream_status;
        }

        location = /auth {
            internal;
            proxy_pass              http://backend/auth-request;
            proxy_pass_request_body off;
            proxy_set_header        Content-Length "";
            proxy_set_header        X-Original-URI $request_uri;
        }
    }
}
```
Alternatively, use the paid version of ELK to gain access to X-Pack, which also adds authentication.

#### An aside: Using log aggregation as an extra test

If you are running end-to-end tests within CI, you can re-purpose your log aggregation stack to ensure no warnings or errors occur while the tests run:
```
FROM vm/ubuntu:18.04

# install docker, etc

RUN docker-compose up -d
RUN docker-compose -f elk.yaml up -d
RUN docker-compose exec web npm run test
RUN docker-compose exec elasticsearch curl -X GET 'http://localhost:9200/logs/_search' | grep -vq error
```

## Examples of log aggregation platforms
---
- ElasticSearch / Logstash / Kibana (ELK)
- Fluentd
- DataDog
- LogDNA
- AWS CloudWatch Logs

## Conclusion
---
Log Aggregation is a key tool for diagnosing problems in production. It's relatively simple to install a turnkey solution like ELK or CloudWatch into a production system, and it makes diagnosing and triaging problems in production significantly easier.
