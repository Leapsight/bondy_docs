---
description: Docker is the preferred way of installing and running Bondy.
---

# Installing using Docker

You can install Bondy by using Docker images. 

Images are available on [Docker Hub](https://hub.docker.com/r/leapsight/bondy). The source files for the images are [available on Gitlab](https://gitlab.com/leapsight/bondy_docker). From Gitlab you can extend and rebuild the images and upload them to your own docker repository.

## Running a Bondy node using docker

You can run an official Bondy Docker image using the `docker run` command with an image name using the following syntax: `leapsight/bondy:{VERSION}[-{VARIANT}] where:`

* `{VERSION}` can be `master`, `develop` or a tag like `0.8.6` 
* `{VARIANT}` can be null or `slim` \(we will provide the `alpine` variant in the future\).

For example to run the 0.8.6 release you would use:

```bash
docker run -d leapsight/bondy:0.8.6
```

To run the slim variant of the same release you would use:

```bash
docker run -d leapsight/bondy:0.8.6-slim
```

### Exposing ports

The docker image exposes the following ports:

| PORT | DESCRIPTION |
| :--- | :--- |
| 18080 | API GATEWAY HTTP and WAMP WS |
| 18081 | ADMIN API HTTP |
| 18082 | WAMP RAW SOCKET TCP |
| 18083 | API GATEWAY HTTPS and WSS |
| 18084 | ADMIN API HTTPS |
| 18085 | WAMP RAW SOCKET TLS |
| 18086 | CLUSTER PEER SERVICE |

In case you need to expose them or want to customise port mapping you would run it like this:

```bash
docker run \
    -p 18080:18080 \
    -p 18081:18081 \
    -p 18082:18082 \
    -p 18086:18086 \
    --name bondy1 \
    -d leapsight/bondy:0.8.6
```

## Configuring a Bondy node

The methods explained above do not allow you to provide a custom `bondy.conf` file and associated files as explained in the [Configuration Reference](../configuring/configuration-reference/) section.

In order to configure Bondy when using Docker you will have two options:

1. Mounting a volume when executing the `docker run` command
2. Creating your own docker image

### Mounting a volume with the config files

First, you will need to create your config files in a local directory e.g. `/tmp/bondy/etc` and map it to the `bondy/etc` directory exposed by the docker image.

Then, you will need to create a at least a minimal configuration for Bondy in that directory. The following are the snippets for a minimal configuration enabling anonymous clients to establish a session:

{% code-tabs %}
{% code-tabs-item title="bondy.conf" %}
```text
distributed_cookie = bondy
nodename = bondy@127.0.0.1
aae.data_exchange_timeout = 1m
aae.enabled = on
security.allow_anonymous_user = on
security.automatically_create_realms = off
security.config_file = $(platform_etc_dir)/security_config.json

```
{% endcode-tabs-item %}

{% code-tabs-item title="security\_config.json" %}
```javascript
[ 
    { 
        "uri" : "com.myapp.test", 
        "description" : "A test realm", 
        "authmethods" : ["wampcra", "ticket", "anonymous"], 
        "security_enabled" : true, 
        "users" : [ 
            "sources" : [ 
                { 
                    "usernames" : "all", 
                    "authmethod" : "password", 
                    "cidr" : "0.0.0.0/0", 
                    "meta" : { 
                        "description" : "Allows all users from any network authenticate using password credentials." 
                    } 
                }, 
                { 
                    "usernames" : "anonymous", 
                    "authmethod" : "trust", 
                    "cidr" : "0.0.0.0/0", 
                    "meta" : { 
                        "description" : "Allows all users from any network authenticate as anonymous." 
                    }
                } 
            ], 
            "grants" : [
                { 
                    "permissions" : [ 
                        "wamp.register", 
                        "wamp.unregister", 
                        "wamp.subscribe", 
                        "wamp.unsubscribe", 
                        "wamp.call", 
                        "wamp.cancel", 
                        "wamp.publish" 
                    ], 
                    "uri" : "*", 
                    "roles" : ["anonymous"] 
                } 
            ] 
        }
    ]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Finally, you can run the docker image by mounting the local directory as the `/bondy/etc` volume adding the option `-v ~/tmp/bondy/etc:/bondy/etc` as shown in the following example:

```bash
docker run \
    -p 18080:18080 \
    -p 18081:18081 \
    -p 18082:18082 \
    -p 18086:18086 \
    --name bondy1 \
    -v ~/tmp/bondy/etc:/bondy/etc \
    -d leapsight/bondy:0.8.6
```

### Creating your own docker image

In order to configure Bondy when using Docker you will need  to create your own custom docker image from the official images or deploy the official image using a container orchestration platform like Kubernetes. 

The section [Configuring Bondy on Docker](../configuring/configuring-bondy-on-docker.md)  explains how to create your a docker image allowing you to provide a custom `bondy.conf` file. [Deploying with Kubernetes](deploying-with-kubernetes.md) explains how to configure and deploy a cluster with Kubernetes.



