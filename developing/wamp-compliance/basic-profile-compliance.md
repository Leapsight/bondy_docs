# Basic Profile Compliance

## General Features

| Feature | Implementation Status | Notes |
| :--- | :--- | :--- |
| Transport and Session Lifetime | Implemented | Each session establishes a new transport connection. |
| Close session and connection on protocol errors | Implemented | As required, Bondy sends an `ABORT` message with error `wamp.error.protocol_violation` |
| JSON Serialization | Implemented |  |
| Msgpack Serialization | Implemented |  |
| Extensibility | Partial | `Options` and `Details` object keys are not validated against regex `[a-z][a-z0-9_]{2,}` for WAMP predefined key, nor `[a-z0-9]{3,}` for custom keys. |
| No Polymorphism, avoid empty arguments and keyword arguments | Implemented |  |
| Session Lifecycle | Implemented |  |
| Agent Identification | Implemented |  |

## PubSub Features

| Feature | Implementation Status | Notes |
| :--- | :--- | :--- |
| Ordering Guarantees | Partial |  |

### Ordering Guarantees

The ordering guarantees are as follows:

If _Subscriber A_ is subscribed to both **Topic 1** and **Topic 2**, and _Publisher B_ first publishes an **Event 1** to **Topic 1**and then an **Event 2** to **Topic 2**, then _Subscriber A_ will first receive **Event 1** and then **Event 2**. This also holds if **Topic 1** and **Topic 2** are identical.

In other words, WAMP guarantees ordering of events between any given _pair_ of Publisher and Subscriber.

Further, if _Subscriber A_ subscribes to **Topic 1**, the `SUBSCRIBED` message will be sent by the _Broker_ to _Subscriber A_ before any `EVENT` message for **Topic 1**.

There is no guarantee regarding the order of return for multiple subsequent subscribe requests. A subscribe request might require the _Broker_ to do a time-consuming lookup in some database, whereas another subscribe request second might be permissible immediately.

## RPC Features

## Non-compliance Cases

### Publish & Subscribe

#### Bondy does not share subscriptions across subscribers

{% tabs %}
{% tab title="Protocol Requirement" %}
The WAMP protocol requires a subscription to be shared amogst subscribers to the same topic. 

A subscription is created when a client sends a subscription request for a topic where there are currently no other subscribers. It is deleted when the last subscriber cancels its subscriptions, or its session is disconnected.

A subscriber receives a subscription ID as the result of a successful subscription request. When an second subscriber issues a subscription request for the same topic, then it receives the **same** subscription ID.
{% endtab %}

{% tab title="Implementation" %}
A subscription is created when a client sends a subscription request for a topic when itself does not have an existing subscription for the same topic. It is deleted when the  subscriber cancels the subscriptions, or its session is disconnected.

A subscriber receives a subscription ID as the result of a successful subscription request. When an second subscriber issues a subscription request for the same topic, then it receives a **different** subscription ID.
{% endtab %}

{% tab title="Rationale" %}
Bondy was designed as a distributed router with continuous availailability as its main goal. Bondy uses an eventually consistent model avoiding coordination between nodes at all cost.

Sharing a subscription between two or more subscribers in at least two cluster nodes will require coordination \(concensus\) and thus we do not support it.
{% endtab %}
{% endtabs %}

### Routed RPC



