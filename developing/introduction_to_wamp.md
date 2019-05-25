---
description: >-
  WAMP is an open standard WebSocket and TCP/IP subprotocol that provides two
  application messaging patterns in one unified protocol: Remote Procedure Calls
  + Publish & Subscribe.
---

# Introduction to WAMP

## What is WAMP?

> The Web Application Messaging Protocol \(WAMP\) is intended to provide application developers with the semantics they need to handle messaging between components in distributed applications.  
> – WAMP Protocol Specification

WAMP is an open standard WebSocket and TCP/IP subprotocol that provides two application messaging patterns in one unified protocol: Remote Procedure Calls + Publish & Subscribe. 

{% hint style="success" %}
Combining these two patterns into a single protocol allows it to be used for the entire messaging requirements of a distributed system, thus reducing technology stack complexity, as well as networking overheads.
{% endhint %}

## Key Characteristics

WAMP is a routed protocol**,**  with all components connecting to a WAMP Router e.g. Bondy, where the WAMP Router performs message routing between the components.

WAMP provides two messaging patterns: [Publish & Subscribe \(PubSub\)](introduction_to_wamp.md#publish-and-subscribe-pubsub) and [Routed Remote Procedure Calls \(RPCs\)](introduction_to_wamp.md#routed-remote-procedure-calls-rpcs).

Using WAMP you can build distributed systems out of application components which are loosely coupled, written in multiple programming languages and communicate in \(soft\) real-time. WAMP clients already exist for multiple languages and is very easy to implement in your preferred language.

### **Publish & Subscribe \(PubSub\)** 

Publish & Subscribe \(PubSub\) is an established messaging pattern where a component, the _Subscriber_, informs the router that it wants to receive information on a topic \(i.e., it subscribes to a topic\). Another component, a _Publisher_, can then publish to this topic, and the router distributes events to all Subscribers.

### **Routed Remote Procedure Calls \(RPCs\)**

Routed Remote Procedure Calls \(RPCs\) rely on the same sort of decoupling that is used by the Publish & Subscribe pattern. A component, the _Callee_, announces to the router that it provides a certain procedure, identified by a procedure name. Other components, _Callers_, can then call the procedure, with the router invoking the procedure on the Callee, receiving the procedure's result, and then forwarding this result back to the Caller. Routed RPCs differ from traditional client-server RPCs in that the router serves as an intermediary between the Caller and the Callee.

## Two flavours: Basic and Advanced Profiles

The WAMP Protocol Specification separated protocol features into two profiles: Basic and Advanced.

This separation into Basic and Advanced Profiles is intended to extend the reach of the protocol. It allows implementations to start out with a minimal, yet operable and useful set of features, and to expand that set from there. It also allows implementations that are tailored for resource-constrained environments, where larger feature sets would not be possible.

{% hint style="info" %}
Advanced Profile features are announced during session establishment, so that different implementations can adjust their interactions to fit the commonly supported feature set.
{% endhint %}

