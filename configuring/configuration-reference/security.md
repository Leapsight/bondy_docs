# Security Settings

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
      <td style="text-align:left">{{platform_etc_dir}}/
        <br />security_config.json</td>
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
</table>## 

