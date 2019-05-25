# Advanced Profile Compliance

## General Features

| Feature | Protocol Status | Compliance Status | Extensions |
| :--- | :--- | :--- | :--- |
| Challenge-response Authentication | beta | Full | No |
| Cookie authentication | beta | Full | No |
| Ticket authentication | beta | Full | No |
| Rawsocket transport | stable | Full | No |
| Batched WS transport | sketch | Planned |  |
| Longpoll transport | beta | Planned |  |
| Session Meta API | beta | Full | Yes |

## PubSub Features

<table>
  <thead>
    <tr>
      <th style="text-align:left">Feature</th>
      <th style="text-align:left">Protocol Status</th>
      <th style="text-align:left">Complicance Status</th>
      <th style="text-align:left">Extensions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">subscriber_blackwhite_listing</td>
      <td style="text-align:left">stable</td>
      <td style="text-align:left">Full</td>
      <td style="text-align:left">No</td>
    </tr>
    <tr>
      <td style="text-align:left">publisher_exclusion</td>
      <td style="text-align:left">stable</td>
      <td style="text-align:left">Full</td>
      <td style="text-align:left">No</td>
    </tr>
    <tr>
      <td style="text-align:left">publisher_identification</td>
      <td style="text-align:left">alpha</td>
      <td style="text-align:left">Full</td>
      <td style="text-align:left">No</td>
    </tr>
    <tr>
      <td style="text-align:left">publication_trustlevels</td>
      <td style="text-align:left">alpha</td>
      <td style="text-align:left">Full</td>
      <td style="text-align:left">No</td>
    </tr>
    <tr>
      <td style="text-align:left">subscription_meta_api</td>
      <td style="text-align:left">beta</td>
      <td style="text-align:left">Full</td>
      <td style="text-align:left">Yes</td>
    </tr>
    <tr>
      <td style="text-align:left">pattern_based_subscription</td>
      <td style="text-align:left">beta</td>
      <td style="text-align:left">
        <p>Partial,</p>
        <p>Wilcard pattern</p>
        <p>not yet implemented</p>
      </td>
      <td style="text-align:left">No</td>
    </tr>
    <tr>
      <td style="text-align:left">sharded_subscription</td>
      <td style="text-align:left">alpha</td>
      <td style="text-align:left">Planned</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">event_history</td>
      <td style="text-align:left">alpha</td>
      <td style="text-align:left">Planned</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">topic_reflection</td>
      <td style="text-align:left">sketch</td>
      <td style="text-align:left">Planned</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## RPC Features

| Feature | Protocol Status | Compliance Status | Notes |
| :--- | :--- | :--- | :--- |
| progressive\_call\_results | beta | Planned |  |
| progressive\_calls | sketch | Planned |  |
| call\_timeout | alpha | Full | No |
| call\_canceling | alpha | Full | No |
| caller\_identification | alpha | Full | No |
| call\_trustlevels | alpha | Full | No |
| registration\_meta\_api | beta | Full | Yes |
| pattern\_based\_registration | beta | Planned |  |
| shared\_registration | beta | Full | Yes |
| sharded\_registration | alpha | Planned |  |
| registration\_revocation | alpha | Planned |  |
| procedure\_reflection | sketch | Planned |  |

