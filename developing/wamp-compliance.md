---
description: >-
  This section explains Bondy copliance to WAMP with details on those cases were
  it deviates and why.
---

# WAMP Compliance

## Non-compliance Cases

### Publish & Subscribe

#### Bondy does not share subscriptions across subscribers

{% tabs %}
{% tab title="Protocol Requirement" %}
The WAMP protocol requires subscription to be shared amogst subscribers to the same topic. 

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





### Remote Procedure Calls

