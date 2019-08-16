# General Settings

## Metadata settings

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
</table>