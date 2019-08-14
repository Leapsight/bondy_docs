# Configuration Reference

## The `bondy.conf` file

Bondy  has a `bondy.conf` configuration file located under the `platform_etc_dir` directory which by default is located under the `/etc` directory if you are using a source install, or in `/bondy/etc` if you are using Docker or `/usr/local/etc` if you used a binary install.

The `bondy.conf` file is used to set a wide variety of configuration options for Bondy.

In addition to the `bondy.conf` file , you can place a `vm.args` configuration file in the same path in which you find `bondy.conf` to configure Bondy's Erlang VM.

{% hint style="danger" %}
### vm.args

Notice that providing your own`vm.args` works differently than providing a `bondy.conf` file. While your `bondy.conf` options are merged with the defaults, thus overriding the defaults for the keys you provide but leaving intact the others, the `vm.args` options are a full replacement of the dynamically generated `vm.args` by Bondy. 

So only use this option if you really know what you are doing. If you really need to do this, we suggest  using Bondy's generated `vm.args` as a base for your customisations.
{% endhint %}

## Security

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
      <td style="text-align:left"><code>on</code> or <code>off</code>
      </td>
      <td style="text-align:left"><code>off</code>
      </td>
    </tr>
  </tbody>
</table>#### Security JSON config file

