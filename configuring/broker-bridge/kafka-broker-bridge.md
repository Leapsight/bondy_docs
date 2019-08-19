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
</table>{% code-tabs %}
{% code-tabs-item title="bondy.conf" %}
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
{% endcode-tabs-item %}
{% endcode-tabs %}

