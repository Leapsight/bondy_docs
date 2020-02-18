# Cluster Settings



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
        <p><b>cluster.peer_port</b>
        </p>
        <p>Defines the IP to use for the cluster TCP connection.</p>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">18086</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.parallelism</b>
        </p>
        <p>Defines the number of TCP connections for the cluster TCP stack.</p>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">1</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.peer_discovery.enabled</b>
        </p>
        <p>Defines whether Bondy should actively search for peer nodes using a defined
          strategy.</p>
      </td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">off</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.peer_discovery.automatic_join</b>
        </p>
        <p>Defines whether Bondy will automatically join a discovered node forming
          a cluster.</p>
      </td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">off</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.peer_discovery.join_retry_interval</b>
        </p>
        <p>Defines the time duration Bondy will wait between automatic join attempts.</p>
      </td>
      <td style="text-align:left">time duration with units, e.g. &apos;10s&apos; for 10 seconds</td>
      <td
      style="text-align:left">5s</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.peer_discovery.polling_interval</b>
        </p>
        <p>Defines the time duration Bondy will wait between polling attempts</p>
      </td>
      <td style="text-align:left">time duration with units, e.g. &apos;10s&apos; for 10 seconds</td>
      <td
      style="text-align:left">10s</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.peer_discovery.timeout</b>
        </p>
        <p>Defines the time duration Bondy will wait for a reponse for a polling
          attempt.</p>
      </td>
      <td style="text-align:left">time duration with units, e.g. &apos;10s&apos; for 10 seconds</td>
      <td
      style="text-align:left">5s</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.peer_discovery.type</b>
        </p>
        <p>Defines the module responsible for implementing the node discovery strategy.</p>
      </td>
      <td style="text-align:left">module name implementing the <code>bondy_peer_discovery</code> behaviour.
        At the moment only bondy_peer_discovery_dns_agent is supported</td>
      <td
      style="text-align:left">bondy_peer_discovery_dns_agent</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>cluster.tls.enabled</b>
      </td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">off</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.tls.certfile</b>
        </p>
        <p>Default cert location for cluster TLS connection.</p>
      </td>
      <td style="text-align:left">path to the file</td>
      <td style="text-align:left">$(platform_etc_dir)/cert.pem</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.tls.keyfile</b>
        </p>
        <p>Default key location for cluster TLS connection</p>
      </td>
      <td style="text-align:left">path to the file</td>
      <td style="text-align:left">$(platform_etc_dir)/key.pem</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.tls.cacertfile</b>
        </p>
        <p>Default signing authority location for cluster TLS connection.</p>
      </td>
      <td style="text-align:left">path to the file</td>
      <td style="text-align:left">$(platform_etc_dir)/cacert.pem</td>
    </tr>
  </tbody>
</table>