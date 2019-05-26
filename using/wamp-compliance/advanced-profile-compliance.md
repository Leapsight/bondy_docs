# Advanced Profile Compliance

## General Features

| Feature | Protocol Status | Compliance Status | Extensions |
| :--- | :--- | :--- | :--- |
| Challenge-response Authentication | beta |  ✔  |  |
| Cookie authentication | beta | ✔  |  |
| Ticket authentication | beta | ✔  |  |
| Rawsocket transport | stable | ✔  |  |
| Batched WS transport | sketch | 🔜  |  |
| Longpoll transport | beta | 🔜  |  |
| Session Meta API | beta | ✔  | ✔  |

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
      <td style="text-align:left">&#x2714;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">publisher_exclusion</td>
      <td style="text-align:left">stable</td>
      <td style="text-align:left">&#x2714;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">publisher_identification</td>
      <td style="text-align:left">alpha</td>
      <td style="text-align:left">&#x2714;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">publication_trustlevels</td>
      <td style="text-align:left">alpha</td>
      <td style="text-align:left">&#x2714;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">subscription_meta_api</td>
      <td style="text-align:left">beta</td>
      <td style="text-align:left">&#x2714;</td>
      <td style="text-align:left">&#x2714;</td>
    </tr>
    <tr>
      <td style="text-align:left">pattern_based_subscription</td>
      <td style="text-align:left">beta</td>
      <td style="text-align:left">
        <p>&#x2714; ,</p>
        <p>Wilcard pattern</p>
        <p>not yet implemented</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">sharded_subscription</td>
      <td style="text-align:left">alpha</td>
      <td style="text-align:left">&#x2714;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">event_history</td>
      <td style="text-align:left">alpha</td>
      <td style="text-align:left">&#x1F51C;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">topic_reflection</td>
      <td style="text-align:left">sketch</td>
      <td style="text-align:left">&#x1F51C;</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## RPC Features

| Feature | Protocol Status | Compliance Status | Notes |
| :--- | :--- | :--- | :--- |
| progressive\_call\_results | beta | 🔜  |  |
| progressive\_calls | sketch | 🔜  |  |
| call\_timeout | alpha | ✔  |  |
| call\_canceling | alpha | ✔  |  |
| caller\_identification | alpha | ✔  |  |
| call\_trustlevels | alpha | ✔  |  |
| registration\_meta\_api | beta | ✔  | ✔  |
| pattern\_based\_registration | beta | 🔜  |  |
| shared\_registration | beta | ✔  | ✔  |
| sharded\_registration | alpha | 🔜  |  |
| registration\_revocation | alpha | 🔜  |  |
| procedure\_reflection | sketch | 🔜  |  |

