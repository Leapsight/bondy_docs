---
description: 'Frequently asked questions about Bondy, its architecture and WAMP.'
---

# FAQs

## General

### How compliant is Bondy to the WAMP protocol?

Please find the answers to this question in the [WAMP Compliance](reference/wamp-compliance/) section.

### How is a WAMP Router different than other messaging technologies?

This is a difficult question to answer as it all depends on your use cases, quality attributes requirements and your architecture design i.e. the way you will solve the trade-offs between all those quality attribute requirements.

In general, WAMP differs from other messaging platforms in that it natively \(and by design\) provides an implementation of routed Remote Procedure Calls \(RPC\) together with Publish & Subscribe.

As is name implies, Publish & Subscribe offers at most once semantics a.k.a fire-and-forget, whereas other messaging platforms provide stronger message delivery guarantees e.g. at least once and exactly once semantics.

Being an extensible protocol means we can extend the message delivery guarantees and we have plans to do so e.g. at least once.

For a further comparison with other products and technologies we invite you to review the [WAMP Compared article](https://wamp-proto.org/comparison.html) in the protocol specification website.

### How is Bondy different than other WAMP routers?

Bondy provides a unique sets of features which sets it apart from other WAMP router implementations in terms of _scalability, reliability, high-performance and operational simplicity_.

Read more about this differences in  [What is Bondy](overview/what-is-bondy.md) section.

## Architecture 

### In which language is Bondy implemented?

Bondy is implemented in Erlang, a wonderful programming language and platform for concurrent and \(soft\) real-time applications.

### Why does Bondy use an eventually consistent model?

Because we need Bondy to be scaleable and always-on either in the case of inter- or intra-datacentre clusters. 

We think it is really stupid to design super scaleable and fault-tolerant backend platforms using NoSQL databases, eventually consistency and more sophisticated techniques like CRDTs only to then define an API layer on top that relies on a strong consistency model. 

This problem usually happens when you use an API Gateway that relies on strong consistency for configuration and/or cluster state data replication,  in most cases by relying on a strong consistency database management system. All the hard work you've done in the backend to provide an always-on system is then hampered by an entry point which is not!

## Data Storage

### Does Bondy depends on an external database server?

No, Bondy does not depend on any external database server. Every Bondy node embeds a database which at the moment is based on Basho's fork of LevelDB but we plan to support and/or migrate to other backends in the future.

### Why does Bondy use its own embedded database?

Because we want to provide an always on platform which is also easy to manage. Most data entities in Bondy are resident in memory to reduce latency e.g. routing tables, authorization checks, access tokens. Using an external database would imply not only the possibility of losing the connection to it, but also the need to instrument a caching layer.

### Can Bondy use an external database for storing its state?

The answer is "not now" for some data entities and "not ever" for some others. 

For example, some data entities could be managed externally and we have plans to enable that capability through plugins e.g. managing user credentials in an external LDAP or database. But for some others it would be in detriment of Bondy's capabilities and the architectural tradeoffs we made for its design. Please refer to [Why does Bondy use its own embedded database?](faqs.md#why-does-bondy-use-its-own-embedded-database).

## License

### How is Bondy licensed?

Leapsight Bondy is licensed under the Apache License 2.0, review a copy of the license [here](https://gitlab.com/leapsight/bondy/blob/develop/LICENSE).

### How is this documentation licensed?

You can find the answer in the [Documentation License](documentation-license.md) page.

## Commercial Support

### Do you provide Commercial Support?

Yes, please contact us to understand the options.



