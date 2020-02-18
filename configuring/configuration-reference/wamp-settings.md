# WAMP Settings

| Key | Acceptable Values | Default |
| :--- | :--- | :--- |
| wamp.tcp.enabled | on \| off | on |
| wamp.tcp.port | integer | 18082 |
| wamp.tcp.acceptors\_pool\_size | integer | 200 |
| wamp.tcp.max\_connections | integer | 100000 |
| wamp.tcp.keepalive | on \| off | on |
| wamp.tcp.nodelay | on \| off | on |
| wamp.tcp.serializers.erl | 4..15 | 15 |
| wamp.tcp.serializers.bert | 4..15 | 4 |
| wamp.tls.enabled | on \| off | off |
| wamp.tls.port | integer | 18085 |
| wamp.tls.acceptors\_pool\_size | integer | 200 |
| wamp.tls.max\_connections | integer | 100000 |
| wamp.tls.keepalive | on \| off | on |
| wamp.tls.nodelay | on \| off | on |
| wamp.tls.backlog | integer | 1024 |
| wamp.tls.certfile | path to a file | $\(platform\_etc\_dir\)/cert.pem |
| wamp.tls.keyfile | path to a file | $\(platform\_etc\_dir\)/key.pem |
| wamp.tls.cacertfile | path to a file | $\(platform\_etc\_dir\)/cacert.pem |

