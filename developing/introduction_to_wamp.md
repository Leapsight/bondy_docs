---
description: >-
  WAMP is an open standard WebSocket and TCP/IP subprotocol that provides two
  application messaging patterns in one unified protocol: Remote Procedure Calls
  + Publish & Subscribe.
---

# Introduction to WAMP

## What is WAMP?

WAMP is an open standard WebSocket and TCP/IP subprotocol that provides two application messaging patterns in one unified protocol: Remote Procedure Calls + Publish & Subscribe. Using WAMP you can build distributed systems out of application components which are loosely coupled, written in multiple programming languages and communicate in \(soft\) real-time. WAMP clients already exist for multiple languages and is very easy to implement in your preferred language.

### **Routed Remote Procedure Calls \(RPCs\)**

In WAMP, software components register individual procedures and any other component can call this via Crossbar.io, with Crossbario handling the registrations, call and result routing.

### **Publish & Subscribe \(PubSub\)** 

components subscribe to topics and publish to these, with Crossbar.io handling the subscriptions and dispatching.

