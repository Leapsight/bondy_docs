# Configuration Reference

## The `bondy.conf` file

Bondy  has a `bondy.conf` configuration file that is used to set a wide variety of _static configuration options_ for Bondy and its location depends on the type of install you are using shown in the following table.

| Install Type | bondy.conf location |
| :--- | :--- |
| Source install | `/etc` |
| Docker Image | `/bondy/etc` |

The `bondy.conf` file is used to set a wide variety of configuration options for Bondy. The file uses a sysctl-like syntax that looks like this:

{% code-tabs %}
{% code-tabs-item title="bondy.conf" %}
```text
nodename = bondy@127.0.0.1
distributed_cookie = bondy
security.allow_anonymous_user = off
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="warning" %}
Notice that for every option not provided by your configuration, Bondy will define a default value \(also specified in the following sections\).
{% endhint %}

## Feature-specific configuration files

Some features and/or subsystems in Bondy  allow providing an additional JSON configuration file e.g. the Security subsystem.

In those cases, we need to let Bondy know where to find those specific files. This is done in the `bondy.conf` under the desired section e.g. the following configuration file adds the location for the `security_conf.json` file.

{% code-tabs %}
{% code-tabs-item title="bondy.conf" %}
```text
nodename = bondy@127.0.0.1
distributed_cookie = bondy
security.allow_anonymous_user = off
security.config_file = /bondy/etc/security_conf.json
```
{% endcode-tabs-item %}
{% endcode-tabs %}

\*\*\*\*

## Advance configuration options

In addition to the `bondy.conf` file , you can place a `vm.args` configuration file in the same path in which you find `bondy.conf` to configure Bondy's Erlang VM.

{% hint style="danger" %}
Notice that providing your own`vm.args` works differently than providing a `bondy.conf` file. While your `bondy.conf` options are merged with the defaults, thus overriding the defaults for the keys you provide but leaving intact the others, the `vm.args` options are a full replacement of the dynamically generated `vm.args` by Bondy. 

So only use this option if you really know what you are doing. If you really need to do this, we suggest  using Bondy's generated `vm.args` as a base for your customisations.
{% endhint %}

## General settings

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
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## Security settings

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
        <p><b>security.config_file</b>
        </p>
        <p>The filename of a security JSON configuration file, which allows you to
          statically configure realms and its users, groups, sources and permissions.</p>
      </td>
      <td style="text-align:left">the path to a file</td>
      <td style="text-align:left">{{platform_etc_dir}}/security_config.json</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>security.automatically_create_realms</b>
        </p>
        <p>Defines whether Bondy create&apos;s a new realm or not when a session
          wants to connect a non existing realm.</p>
      </td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">off</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>security.allow_anonymous_user</b>
        </p>
        <p>Defines whether Bondy allows the &quot;anonymous&quot; user</p>
      </td>
      <td style="text-align:left">on | off</td>
      <td style="text-align:left">on</td>
    </tr>
  </tbody>
</table>## Cluster settings

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
        <p>Defines the IP to use for the cluster TCP
          <br />connection.</p>
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
        <p>Defines the time duration Bondy will wait
          <br />between automatic join attempts.</p>
      </td>
      <td style="text-align:left">time duration with units,
        <br />e.g. &apos;10s&apos; for 10 seconds</td>
      <td style="text-align:left">5s</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.peer_discovery.polling_interval</b>
        </p>
        <p>Defines the time duration Bondy will wait
          <br />between polling attempts</p>
      </td>
      <td style="text-align:left">time duration with units,
        <br />e.g. &apos;10s&apos; for 10 seconds</td>
      <td style="text-align:left">10s</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.peer_discovery.timeout</b>
        </p>
        <p>Defines the time duration Bondy will wait for a reponse for a polling
          attempt.</p>
      </td>
      <td style="text-align:left">time duration with units,
        <br />e.g. &apos;10s&apos; for 10 seconds</td>
      <td style="text-align:left">5s</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>cluster.peer_discovery.type</b>
        </p>
        <p>Defines the module responsible for
          <br />implementing the node discovery strategy.</p>
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