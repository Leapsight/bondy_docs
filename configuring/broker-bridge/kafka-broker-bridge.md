# Kafka Broker Bridge Settings

## Supported parameters

All parameters explained below should be prefixed by `broker_bridge.kafka` e.g. `broker_bridge.kafka.enabled`.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Accepts</th>
      <th style="text-align:left">Default</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>enabled</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>clients.&lt;name&gt;.allow_topic_auto_creation</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">off</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>clients.&lt;name&gt;.auto_start_producers</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">on</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>clients.&lt;name&gt;.endpoints</code>
      </td>
      <td style="text-align:left">
        <p>[ {IPString, PortNumber} ]
          <br />e.g.[{&quot;127.0.0.1&quot;, 9092}]</p>
        <p>(*)</p>
      </td>
      <td style="text-align:left">none</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>clients.default.max_metadata_sock_retry</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>{% tabs %}
{% tab title="bondy.conf" %}
```bash
broker_bridge.config_file = $(platform_etc_dir)/broker_bridge_config.json
broker_bridge.kafka.enabled = on
broker_bridge.kafka.clients.default.allow_topic_auto_creation = off
broker_bridge.kafka.clients.default.auto_start_producers = on
broker_bridge.kafka.clients.default.endpoints = [{"127.0.0.1", 9092}]
broker_bridge.kafka.clients.default.max_metadata_sock_retry = 5
broker_bridge.kafka.clients.default.producer.partition_restart_delay_seconds = 2s
broker_bridge.kafka.clients.default.producer.required_acks = 1
broker_bridge.kafka.clients.default.producer.topic_restart_delay_seconds = 10s
broker_bridge.kafka.clients.default.reconnect_cool_down_seconds = 10s
broker_bridge.kafka.clients.default.restart_delay_seconds = 10s
broker_bridge.kafka.topics.account_events = ${MAGENTA_ACCOUNT_EVENTS_TOPIC}
broker_bridge.kafka.topics.user_events = ${MAGENTA_USER_EVENTS_TOPIC}
```
{% endtab %}
{% endtabs %}

## Kafka Bridge Subscriptions Specification Format Extensions

### Action Object

| Property | Required | Type | Description | Examples |
| :--- | :--- | :--- | :--- | :--- |
| **id** | true | string | A unique identifier for this specification | subscribers\_1 |
| **meta** | false | object | An arbitrary object containing user metadata. Bondy treats it as an opaque object. | {"foo" : "bar"} |
| **subscriptions** | true |  |  |  |

The following snippet provides an example subscriptions using the defined Action Object.

{% tabs %}
{% tab title="/bondy/etc/subscriptions.json" %}
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
{% endtab %}
{% endtabs %}

