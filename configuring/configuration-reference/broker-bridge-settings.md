# Broker Bridge Configuration

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
        <p>The configuration filename for the Broker Bridge.</p>
      </td>
      <td style="text-align:left">path to a file</td>
      <td style="text-align:left">$(platform_etc_dir)/
        <br />broker_bridge_config.json</td>
    </tr>
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
      <td style="text-align:left">string</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.clients.$name.endpoints</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.clients.$name.restart_delay_seconds</td>
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
      <td style="text-align:left">broker_bridge.kafka.clients.$name.reconnect_cool_down_seconds</td>
      <td
      style="text-align:left">a time duration with units, e.g. &apos;10s&apos; for 10 seconds</td>
        <td
        style="text-align:left">10s</td>
    </tr>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.clients.$name.auto_start_producers</td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">on</td>
    </tr>
    <tr>
      <td style="text-align:left">broker_bridge.kafka.clients.$name.allow_topic_auto_creation</td>
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
      <td style="text-align:left">broker_bridge.kafka.clients.$name.producer.required_acks</td>
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