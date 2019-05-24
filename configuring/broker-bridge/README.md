---
description: >-
  A subsystem that enables to manage WAMP subscriptions that are re-published to
  an external non-WAMP broker.
---

# Broker Bridge

Bondy Broker Bridge is a substem that acts as an anonymous WAMP subscriber allowing Bondy to re-publish events to an external message broker.

The subsytem manages a set of bridges, each one enabled through the `bondy.conf` file. At the moment the `bondy_kafka_bridge` is the only one provided and diabled by default.

To enable the Kafka Bridge modifiy the `broker_bdirge.kafka.enabled` option as shown below:

```erlang
broker_bridge.kafka.enabled = on
```

To learn more about the Kafka Bridge and how to configure it, read the following section:

{% page-ref page="kafka-broker-bridge.md" %}

## Configuring Subscriptions

A subscription can be dynamically created and removed at runtime using the HTTP and WAMP APIs or it can be created at Bondy initialisation time through a configuration file.

### Configuring Subscriptions via a configuration file

To configure one or more subscriptions you need to modify the `bondy.conf` to tell Bondy where to find the Subscriptions configuration using Broker Bridge Subscription Configuration format.

The following tells Bondy to find and load the subcribers specified in the `data/subscribers.json` file.

{% code-tabs %}
{% code-tabs-item title="bondy.conf" %}
```text
bondy_broker_bridge.config_file = /data/subscriptions.json
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The following snippet provides an example 

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
                "realm_uri": "com.example.realm",
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

