# Configuration Reference

Bondy  has a `bondy.conf` configuration file located in `/etc` if you are using a source install or in `/etc/bondy` or `/usr/local/etc` if you used a binary install.

The `bondy.conf` file is used to set a wide variety of configuration options for a Bondy node.

## The advanced.config file

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
      <td style="text-align:left">$(platform_etc_dir)/security_config.json</td>
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

