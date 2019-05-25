# Basic Profile Compliance

## General Features

| Feature | Compliance Status | Extensions |
| :--- | :--- | :--- |
| Transport and Session Lifetime | Full, Each session establishes a new transport connection. | No |
| Close session and connection on protocol errors | Full | No |
| Serialization \(JSON and Msgpack\) | Full | Yes |
| Validation of custom object keys using regex `[a-z0-9]{3,}` | Planned |  |
| No Polymorphism, avoid empty arguments and keyword arguments | Full | No |
| Session Lifecycle | Full | No |
| Agent Identification | Full | No |



## PubSub Features

<table>
  <thead>
    <tr>
      <th style="text-align:left">Feature</th>
      <th style="text-align:left">Implementation Status</th>
      <th style="text-align:left">Extensions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Ordering Guarantees</td>
      <td style="text-align:left">Partial, see <a href="basic-profile-compliance.md#nc-1-pubsub-ordering-guarantees">NC1</a>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p>Subscription (and Subscription ID) to be shared amongst subscribers to
          the same topic.</p>
      </td>
      <td style="text-align:left">Partial, see <a href="basic-profile-compliance.md#nc-2-bondy-does-not-share-subscriptions-across-subscribers">NC2</a>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>### NC1: PubSub Ordering Guarantees

{% tabs %}
{% tab title="Requirement" %}
The ordering guarantees are as follows:

If _Subscriber A_ is subscribed to both **Topic 1** and **Topic 2**, and _Publisher B_ first publishes an **Event 1** to **Topic 1**and then an **Event 2** to **Topic 2**, then _Subscriber A_ will first receive **Event 1** and then **Event 2**. This also holds if **Topic 1** and **Topic 2** are identical.

In other words, WAMP guarantees ordering of events between any given _pair_ of Publisher and Subscriber.

Further, if _Subscriber A_ subscribes to **Topic 1**, the `SUBSCRIBED` message will be sent by the _Broker_ to _Subscriber A_ before any `EVENT` message for **Topic 1**.

There is no guarantee regarding the order of return for multiple subsequent subscribe requests. A subscribe request might require the _Broker_ to do a time-consuming lookup in some database, whereas another subscribe request second might be permissible immediately.
{% endtab %}

{% tab title="Implementation" %}

{% endtab %}

{% tab title="Rationale" %}

{% endtab %}

{% tab title="Roadmap" %}

{% endtab %}
{% endtabs %}

### NC2: Bondy does not share subscriptions across subscribers

{% tabs %}
{% tab title="Requirement" %}
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

{% tab title="Roadmap" %}
No plans to change the implementation.
{% endtab %}
{% endtabs %}

## RPC Features



