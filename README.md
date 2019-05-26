---
description: >-
  Welcome to the documentation for Bondy. Here you can learn about key Bondy
  concepts, find quick starts, reference material, tutorials and more.
---

# Welcome

## What is Bondy?

> Leapsight Bondy is an open source, scalable networking platform for distributed miicroservices _\(µServices\)_ and _Internet Of Things \(IoT\)_ applications written in Erlang. Bondy implements the open Web Application Messaging Protocol \(WAMP\) offering both PubSub and routed RPC.

As opposed to other API management solutions, Bondy unifies Remote Procedure Call \(RPC\) and Publish-Subscribe messaging patterns over multiple transports under a single layer, implementing the open [Web Application Messaging Protocol \(WAMP\)](using/introduction_to_wamp.md).

Becuase it implements WAMP, Bondy enables loosely coupled application components \(embedded software, µServices, mobile and web applications\) to communicate in \(soft\) real-time.

Bondy enables a polyglot architecture. It routes messages between those application components, which can be written in any language as long as they implement the WAMP protocol.

## How is Bondy different than other WAMP routers?

Bondy provides a unique sets of features which sets it apart from other WAMP router implementations in terms of _scalability, reliability, high-performance and operational simplicity_.

* **Distributed by design** – ****As opposed to existing WAMP Router implementations, Bondy was designed as reliable distributed router, ensuring continued operation in the event of node or network failures through clustering and data replication. 
* **Scalability** – Bondy is written in Erlang/OTP which provides the underlying operating system to handle concurrency and scalability requirements, allowing Bondy to scale to millions of concurrent connections.
* **Peer-to-peer master-less clustering** – All nodes in a Bondy cluster are equal, thanks to the underlying clustering and networking technology which provides a master-less architecture.
* **Low latency data replication** – All nodes in a Bondy cluster share a global state which is replicated through a highly scaleable and low latency eventually consistency model based on gossip. The underlying technology enables various network topologies which supports large clusters \(the underlying technology has been demonstrated to scale up to 1,024 nodes\). 
* **Ease of use** – Bondy is easy to operate due to its operational simplicity provided by its peer-to-peer nature and the lack of special nodes, the automatic data replication and self-healing.
* **Embedded REST API Gateway** – Bondy embeds a powerful API Gateway that can translate HTTP REST actions to WAMP RPC and PubSub operations. The API Gateway leverages the underlying storage and replication technology to deploy the API Specifications to the cluster nodes ni real-time.
* **Embedded Role-based Access Control \(RBAC\)** – Bondy embeds a RBAC subsystem to empower the per realm API Gateway OAuth2 and WAMP security features. It borrows its design and implementation from Riak Core's Security subsystem which itself was modelled after PostgreSQL RBAC.

{% hint style="warning" %}
In the current release the security system is just used for authentication and not authorization. Work is on the way to implement authorization in the next release.
{% endhint %}

## How is a WAMP Router different than other technologies?



