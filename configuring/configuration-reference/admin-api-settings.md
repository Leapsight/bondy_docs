# Admin API Configuration

| Key | Acceptable Values | Default |
| :--- | :--- | :--- |
| admin\_api.http.enabled | on \| off | on |
| admin\_api.http.acceptors\_pool\_size | integer | 200 |
| admin\_api.http.max\_connections | integer | 250000 |
| admin\_api.http.keepalive | on \| off | off |
| admin\_api.http.nodelay | on \| off | on |
| admin\_api.http.backlog | integer | 1024 |
| admin\_api.https.enabled | on \| off | off |
| admin\_api.https.acceptors\_pool\_size | integer | 200 |
| admin\_api.https.max\_connections | integer | 250000 |
| admin\_api.https.keepalive | on \| off | off |
| admin\_api.https.nodelay | on \| off | on |
| admin\_api.https.backlog | integer | 4096 |
| admin\_api.https.certfile | the path to a file | $\(platform\_etc\_dir\)/cert.pem |
| admin\_api.https.keyfile | the path to a file | $\(platform\_etc\_dir\)/key.pem |
| admin\_api.https.cacertfile | the path to a file | $\(platform\_etc\_dir\)/cacert.pem |
|  |  |  |

