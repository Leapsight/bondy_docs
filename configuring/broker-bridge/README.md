---
description: >-
  A subsystem that enables to manage WAMP subscriptions that are re-published to
  an external non-WAMP broker.
---

# Broker Bridge

Bondy Broker Bridge is a substem that acts as an anonymous WAMP subscriber allowing Bondy to re-publish events to an external message broker.

The subsytem manages a set of bridges, each one enabled through the `bondy.conf` file. At the moment the `bondy_kafka_bridge` is the only one provided and diabled by default.

To enable the Kafka Bridge modifiy the `broker_bridge.kafka.enabled` option as shown below:

```erlang
broker_bridge.kafka.enabled = on
```

To learn more about the Kafka Bridge and how to configure it, read the following section:

{% page-ref page="kafka-broker-bridge.md" %}

## Configuring Subscriptions

A subscription can be dynamically created and removed at runtime using the HTTP and WAMP APIs or it can be created at Bondy initialisation time through a [Bridge Subscription Specification Format](./#bridge-subscriptions-specification-format).

### Configuring Subscriptions via a configuration file

To configure one or more subscriptions you need to modify the `bondy.conf` to tell Bondy where to find a specification file using the [Bridge Subscriptions Specification Format](./#bridge-subscriptions-specification-format).

{% code-tabs %}
{% code-tabs-item title="bondy.conf" %}
```text
bondy_broker_bridge.config_file = /data/subscriptions.json
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The following snippet provides an example subscriptions specification file.

{% code-tabs %}
{% code-tabs-item title="/data/subscriptions.json" %}
```javascript
{
    "id":"subscribers_1",
    "meta":{},
    "subscriptions" : [
        {
            "bridge": "bondy_kafka_bridge",
            "match": {
                "realm": "com.example.realm",
                "topic" : "com.example.user.created",
                "options": {"match": "exact"}
            },
            "action": {
                "type": "produce_sync",
                "topic": "{{kafka.topics |> get(com.magenta.wamp_events)}}",
                "key": "\"{{event.topic}}/{{event.publication_id}}\"",
                "value": "{{event}}",
                "options" : {
                    "client_id": "default",
                    "acknowledge": true,
                    "required_acks": "all",
                    "partition": null,
                    "partitioner": {
                        "algorithm": "fnv32a",
                        "value": "\"{{event.topic}}/{{event.publication_id}}\""
                    },
                    "encoding": "json"
                }
            }
        }
    ]
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Bridge Subscriptions Specification Format

### Specification Object

| Property | Required | Type | Description | Examples |
| :--- | :--- | :--- | :--- | :--- |
| **id** | true | string | A unique identifier for this specification | subscribers\_1 |
| **meta** | false | object | An arbitrary object containing user metadata. Bondy treats it as an opaque object. | {"foo" : "bar"} |
| **subscriptions** | true | array | An array of Subscription Object |  |

### Subscription Object

| Property | Required | Type | Description | Examples |
| :--- | :--- | :--- | :--- | :--- |
| **bridge** | true | Bridge Identifier | The identifier of the bridge to use. These are the Erlang module names of the implemented bridges. | bondy\_kafka\_bridge |
| **match** | true | Match Object |  |  |
| **action** | true | Action Object |  |  |

### Match Object

| Property | Required | Type | Description | Examples |
| :--- | :--- | :--- | :--- | :--- |
| **realm** | true | string | The bondy realm this subscription will live in | my\_realm, com.example.realm |
| **topic** | true | string | The WAMP topic we want to match | com.example.user.added |
| **match** | false | string | The way we want to match the topic. It should be one of "exact", "prefix" or "wildcard" | exact |

{% hint style="warning" %}
At the moment Bondy does not support `wilcard` matching. Support is planned.
{% endhint %}

### Action Object

The Action Object is and abstract object. Concrete implementations are defined by each Bridge.

Review the following link for the Kafka Bridge implementation.

{% page-ref page="kafka-broker-bridge.md" %}





