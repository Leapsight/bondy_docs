---
description: >-
  Docker is the preferred way of running Bondy. Leapsight provides Official
  Docker images for Bondy.
---

# Running with Docker

{% hint style="info" %}
Bondy Docker images are defined in  [bondy\_docker](https://gitlab.com/leapsight/bondy_docker) git repository and the images are published in [Docker Hub](https://hub.docker.com/r/leapsight/bondy) under the `leapsight/bondy` namespace.
{% endhint %}

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

## Configuring a Bondy node using Docker

The methods explained above do not allow you to provide a custom `bondy.conf` file and associated files as explained in the [Configuration Reference](../configuring/configuration-reference.md) section.

In order to configure Bondy when using Docker you will need  to create your own custom docker image from the official images. This is explained in [Configuring Bondy on Docker](../configuring/configuring-bondy-on-docker.md).



