---
description: >-
  Welcome to the documentation for Bondy. Here you can learn about key Bondy
  concepts, find quick starts, reference material, tutorials and more.
---

# Welcome

## What is Bondy?

_Bondy is an open-source high-performance and scalable all-in-one API Management, Gateway and Networking Bus Platform specially designed for the requirements of distributed architectures based on microservices \(µServices\) and the dynamics of Cloud and Internet Of Things \(IoT\) applications._

As opposed to other API management solutions, Bondy unifies Remote Procedure Call \(RPC\) and Publish-Subscribe messaging patterns over multiple transports under a single layer, implementing the open Web Application Messaging Protocol \(WAMP\).

Becuase it used WAMP, Bondy enables loosely coupled application components \(embedded software, µServices, mobile and web applications\) to communicate in \(soft\) real-time.

Bondy enables a polyglot architecture. It routes messages between those application components, which can be written in any language as long as they implement the WAMP protocol.

## How is Bondy different than other WAMP routers?

Bondy provides a unique sets of features which sets it apart from other WAMP router implementations in terms of _scalability, reliability, high-performance and operational simplicity_.

* **Distributed by design** – ****As opposed to existing WAMP Router implementations, Bondy was designed as reliable distributed router, ensuring continued operation in the event of node or network failures through clustering and data replication. 
* **Scalability** – Bondy is written in Erlang/OTP which provides the underlying operating system to handle concurrency and scalability requirements, allowing Bondy to scale to millions of concurrent connections.
* **Peer-to-peer master-less clustering** – All nodes in a Bondy cluster are equal, thanks to the underlying clustering and networking technology which provides a master-less architecture.
* **Low latency data replication** – All nodes in a Bondy cluster share a global state which is replicated through a highly scaleable and low latency eventually consistency model based on gossip. The underlying technology enables various network topologies which supports large clusters \(the underlying technology has been demonstrated to scale up to 1,024 nodes\). 
* **Ease of use** – Bondy is easy to operate due to its operational simplicity provided by its peer-to-peer nature and the lack of special nodes, the automatic data replication and self-healing.



## How is a WAMP Router different than other technologies?



