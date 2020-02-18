---
description: >-
  The following documents the General Settings that can be used in the
  bondy.conf file.
---

# General Configuration

## Coordinated Startup / Shutdown

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Key</b>
      </th>
      <th style="text-align:left"><b>Acceptable Values</b>
      </th>
      <th style="text-align:left"><b>Default</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><b>startup.wait_for_store_partitions</b>
        </p>
        <p>Defines whether Bondy will wait for the db
          <br />partitions to be initialised before
          <br />continuing with initialisation.
          <br />This is automatically turned on in case the
          <br />property startup.wait_for_store_hashtrees is on.</p>
      </td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">on</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>startup.wait_for_store_hashtrees</b>
        </p>
        <p>Defines whether Bondy will wait for the db
          <br />hashtrees to be built before
          <br />continuing with initialisation. In order for the
          <br />hashtrees to be build the property</p>
        <p>aae_enabled needs to be on.</p>
        <p>This is automatically turned on in case the
          <br />property startup.wait_for_store_aae_exchange is on.</p>
      </td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">on</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>startup.wait_for_store_aae_exchange</b>
        </p>
        <p>Defines whether Bondy will wait for the first
          <br />active anti-entropy (AAE) exchange to be finished
          <br />before continuing with initialisation.</p>
        <p>In order for the AAE exchange to be executed</p>
        <p>the property aae_enabled needs to be on.</p>
      </td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">on</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>shutdown_grace_period</b>
        </p>
        <p>The period in seconds that Bondy will wait for clients
          <br />to gracefully terminate their connections when the
          <br />router is shutting down.</p>
      </td>
      <td style="text-align:left">a time duration with units
        <br />e.g. &apos;10s&apos; for 10 seconds</td>
      <td style="text-align:left">30s</td>
    </tr>
  </tbody>
</table>## Erlang VM settings

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
        <p><b>nodename</b>
        </p>
        <p>Name of the Erlang node.</p>
      </td>
      <td style="text-align:left">text</td>
      <td style="text-align:left">bondy@127.0.0.1</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>distributed_cookie</b>
        </p>
        <p>Cookie for distributed node communication.
          <br />All nodes in the same cluster should use the
          <br />same cookie or they will not be able to
          <br />communicate.</p>
      </td>
      <td style="text-align:left">text</td>
      <td style="text-align:left">bondy</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>erlang.async_threads</b>
        </p>
        <p>Sets the number of threads in async thread pool.
          <br />If thread support is available, the default is 64.</p>
        <p>More information at: <a href="http://erlang.org/doc/man/erl.html">http://erlang.org/doc/man/erl.html</a>
        </p>
      </td>
      <td style="text-align:left">integer
        <br />between 0 and 1024</td>
      <td style="text-align:left">64</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>erlang.max_ports</b>
        </p>
        <p>The number of concurrent ports/sockets.</p>
      </td>
      <td style="text-align:left">integer between 1024 and 134217727</td>
      <td style="text-align:left">65536</td>
    </tr>
  </tbody>
</table>