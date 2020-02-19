# Broker Bridge Configuration

## General Configuration

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Acceptable Values</th>
      <th style="text-align:left">Default</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><b>broker_bridge.config_file</b>
        </p>
        <p>The configuration filename for the Broker Bridge.
          <br />Read the <a href="../broker-bridge/#statically-configuring-subscriptions-via-a-configuration-file">Broker Bridge Settings </a>section
          on the specification file format.</p>
      </td>
      <td style="text-align:left">path to a file</td>
      <td style="text-align:left">$(platform_etc_dir)/
        <br />broker_bridge_config.json</td>
    </tr>
  </tbody>
</table>## Kafka Bridge Configuration

The following shows an example configuration for a Kafka bridge.

{% code title="bondy.conf" %}
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
{% endcode %}

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Acceptable Values</th>
      <th style="text-align:left">Default</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.enabled</td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">off</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>broker_bridge.kafka.topics.$name</b>
        </p>
        <p>A mapping of Clients to Kafka topics.
          <br />This mapping is used by the JSON
          <br />broker_bridge.config_file which defines the
          <br />subscribers for each bridge.</p>
        <p></p>
      </td>
      <td style="text-align:left">a list of erlang tuples</td>
      <td style="text-align:left">[{&quot;127.0.0.1&quot;, 9092}]</td>
    </tr>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.clients.$name.endpoints</td>
      <td style="text-align:left">list of</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>broker_bridge.kafka.clients.$name.restart_delay_seconds</b>
        </p>
        <p>How long to wait between attempts to restart the Kafka</p>
        <p>client process when it crashes.</p>
      </td>
      <td style="text-align:left">a time duration with units, e.g. &apos;10s&apos; for 10 seconds</td>
      <td
      style="text-align:left">10s</td>
    </tr>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.clients.$name.max_metadata_sock_retry</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">5</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>broker_bridge.kafka.clients.$name.reconnect_cool_down_seconds</b>
        </p>
        <p>Delay this configured number of seconds before retrying to</p>
        <p>estabilish a new connection to the kafka partition leader.</p>
      </td>
      <td style="text-align:left">a time duration with units, e.g. &apos;10s&apos; for 10 seconds</td>
      <td
      style="text-align:left">10s</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>broker_bridge.kafka.clients.$name.allow_topic_auto_creation</b>
        </p>
        <p>By default, the Kafka client respects what is configured in the broker</p>
        <p>about topic auto-creation. i.e. whether `auto.create.topics.enable&apos;
          <br
          />is set in the broker configuration. However if this parameter is set
          <br
          />to false, the client will avoid sending metadata requests that</p>
        <p>may cause an auto-creation of the topic regardless of what</p>
        <p>the broker config is.</p>
      </td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">on</td>
    </tr>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.clients.$name.producer.topic_restart_delay_seconds</td>
      <td
      style="text-align:left">a time duration with units, e.g. &apos;10s&apos; for 10 seconds</td>
        <td
        style="text-align:left">10s</td>
    </tr>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.clients.$name.producer.partition_restart_delay_seconds</td>
      <td
      style="text-align:left">a time duration with units, e.g. &apos;10s&apos; for 10 seconds</td>
        <td
        style="text-align:left">10s</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>broker_bridge.kafka.clients.$name.producer.required_acks</b>
        </p>
        <p>How many acknowledgements the Kafka broker should receive</p>
        <p>from the clustered replicas before acknowledging producer.
          <br />
          <br />0: the broker will not send any response (this is the only case</p>
        <p>where the broker will not reply to a request)
          <br />
          <br />1: The leader will wait the data is written to the local log</p>
        <p>before sending a response.
          <br />
          <br />-1: If it is -1 the broker will block until the message is</p>
        <p>committed by all in sync replicas before acknowledging.</p>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">1</td>
    </tr>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.clients.$name.socket.sndbuf</td>
      <td style="text-align:left">bytesize</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.clients.$name.socket.recbuf</td>
      <td style="text-align:left">bytesize</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>