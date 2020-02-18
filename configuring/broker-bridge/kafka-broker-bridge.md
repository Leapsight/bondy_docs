# Kafka Broker Bridge Settings

## Kafka Bridge Subscriptions Specification Format Extensions

### Action Object

| Property | Required | Type | Description | Examples |
| :--- | :--- | :--- | :--- | :--- |
| **id** | true | string | A unique identifier for this specification | subscribers\_1 |
| **meta** | false | object | An arbitrary object containing user metadata. Bondy treats it as an opaque object. | {"foo" : "bar"} |
| **subscriptions** | true |  |  |  |

The following snippet provides an example subscriptions using the defined Action Object.

{% code title="/bondy/etc/subscriptions.json" %}
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
{% endcode %}

