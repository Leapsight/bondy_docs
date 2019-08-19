---
description: >-
  A subsystem that enables to re-publish WAMP Events to an external non-WAMP
  broker.
---

# Broker Bridge Settings

{% hint style="info" %}
#### Bondy Broker Bridge is a subsystem that enables you to have a set of supervised embedded WAMP subscribers that re-publish events to an external message broker or system.
{% endhint %}

The subsystem manages a set of bridges, each one enabled through the `bondy.conf` file.   
At the moment the `bondy_kafka_bridge` is the only one provided and it is disabled by default.

## Enabling the Kafka Bridge

To enable the Kafka Bridge modify the `broker_bridge.kafka.enabled` option in the `bondy.conf` file as shown below:

```erlang
broker_bridge.kafka.enabled = on
```

To learn more about the Kafka Bridge and how to configure it, read the following section:

{% page-ref page="kafka-broker-bridge.md" %}

## Configuring Broker Bridge Subscriptions

A subscription can be dynamically created and removed at runtime using the HTTP and WAMP APIs or it can be created at Bondy initialisation time through a [Bridge Subscriptions Specification Format](./#bridge-subscriptions-specification-format).

### Dynamically configuring subscriptions

TBD

{% tabs %}
{% tab title="WAMP" %}

{% endtab %}

{% tab title="HTTP/REST" %}

{% endtab %}
{% endtabs %}

### Statically configuring subscriptions via a configuration file

To configure one or more subscriptions you need to define a specification file using the [Bridge Subscriptions Specification Format](./#bridge-subscriptions-specification-format) and modify the `bondy.conf` to tell Bondy where to find it.

The following snippet provides an example subscriptions specification file.

{% code-tabs %}
{% code-tabs-item title="/bondy/etc/subscriptions.json" %}
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

The following snippet shows how to modify the `bondy.conf` file to tell Bondy where to locate the file.

{% code-tabs %}
{% code-tabs-item title="bondy.conf" %}
```text
bondy_broker_bridge.config_file = /bondy/etc/subscriptions.json
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Broker Bridge Subscriptions Specification Format

### Specification Object

| Property | Required | Type | Description | Examples |
| :--- | :--- | :--- | :--- | :--- |
| **id** | true | string | A unique identifier for this specification | subscribers\_1 |
| **meta** | false | object | An arbitrary object containing user metadata. Bondy treats it as an opaque object. | {"foo" : "bar"} |
| **subscriptions** | true | array | An array of [Subscription Objects](./#subscription-object) |  |

### Subscription Object

| Property | Required | Type | Description | Examples |
| :--- | :--- | :--- | :--- | :--- |
| **bridge** | true | Bridge Identifier | The identifier of the bridge to use. These are the Erlang module names of the implemented bridges. | bondy\_kafka\_bridge |
| **match** | true | [Match Specification Object](./#match-specification-object) |  |  |
| **action** | true | [Action Object](./#action-object) |  |  |

### Match Specification Object

| Property | Required | Type | Description | Examples |
| :--- | :--- | :--- | :--- | :--- |
| **realm** | true | string | The bondy realm this subscription will live in | my\_realm, com.example.realm |
| **topic** | true | string | The WAMP topic we want to match | com.example.user.added |
| **options** | false | [Match Options Object](./#match-options-object) | The way we want to match the topic. It should be one of "exact", "prefix" or "wildcard" | {"match": "exact"} |

### Match Options Object

This the WAMP Subscription Options object.

| Property | Required | Type | Description | Examples |
| :--- | :--- | :--- | :--- | :--- |
| **match** | false | string | The way we want to match the topic. It should be one of "exact", "prefix" or "wildcard" | exact |
| nkey |  |  |  |  |

{% hint style="warning" %}
At the moment Bondy does not support `wildcard` matching. Support is planned.
{% endhint %}

### Action Object

The Action Object is and abstract object. Concrete implementations are defined by each Bridge.

Review the following link for the Kafka Bridge implementation.

{% page-ref page="kafka-broker-bridge.md" %}





