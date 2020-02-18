# REST API Gateway Configuration

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
      <td style="text-align:left">api_gateway.http.acceptors_pool_size</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">200</td>
    </tr>
    <tr>
      <td style="text-align:left">api_gateway.http.max_connections</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">500000</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>api_gateway.config_file</b>
        </p>
        <p>The filename of a the API Gateway JSON configuration file,
          <br />which allows you to statically configure the API Gateway
          <br />with a list of API Specifications.</p>
      </td>
      <td style="text-align:left">path to a file</td>
      <td style="text-align:left">$(platform_etc_dir)/
        <br />api_gateway_config.json</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>api_gateway.http.keepalive</b>
        </p>
        <p>Enables/disables periodic transmission on a connected socket when no other
          data is exchanged. If the other end does not respond, the connection is
          considered broken and an error message is sent to the controlling process.</p>
      </td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">off</td>
    </tr>
    <tr>
      <td style="text-align:left">api_gateway.http.nodelay</td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">on</td>
    </tr>
    <tr>
      <td style="text-align:left">api_gateway.http.backlog</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">4096</td>
    </tr>
    <tr>
      <td style="text-align:left">api_gateway.https.acceptors_pool_size</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">200</td>
    </tr>
    <tr>
      <td style="text-align:left">api_gateway.https.max_connections</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">500000</td>
    </tr>
    <tr>
      <td style="text-align:left">api_gateway.https.keepalive</td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">off</td>
    </tr>
    <tr>
      <td style="text-align:left">api_gateway.https.certfile</td>
      <td style="text-align:left">path to a file</td>
      <td style="text-align:left">$(platform_etc_dir)/
        <br />cert.pem</td>
    </tr>
    <tr>
      <td style="text-align:left">api_gateway.https.keyfile</td>
      <td style="text-align:left">path to a file</td>
      <td style="text-align:left">$(platform_etc_dir)/
        <br />key.pem</td>
    </tr>
    <tr>
      <td style="text-align:left">api_gateway.https.cacertfile</td>
      <td style="text-align:left">path to a file</td>
      <td style="text-align:left">$(platform_etc_dir)/
        <br />cacert.pem</td>
    </tr>
  </tbody>
</table>