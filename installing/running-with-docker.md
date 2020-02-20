---
description: Docker is the preferred way of installing and running Bondy.
---

# Installing using Docker

You can install Bondy by using Docker images. 

Images are available on [Docker Hub](https://hub.docker.com/r/leapsight/bondy). The source files for the images are [available on Gitlab](https://gitlab.com/leapsight/bondy_docker). From Gitlab you can extend and rebuild the images and upload them to your own docker repository.

## Running a Bondy node using docker

You can run an official Bondy Docker image using the `docker run` command with an image name using the following syntax: `leapsight/bondy:{VERSION}[-{VARIANT}] where:`

* `{VERSION}` can be `master`, `develop` or a tag like `0.8.8` 
* `{VARIANT}` can be null or `slim` \(we will provide the `alpine` variant in the future\).

For example to run the 0.8.6 release you would use:

```bash
docker run -d leapsight/bondy:0.8.8
```

To run the slim variant of the same release you would use:

```bash
docker run -d leapsight/bondy:0.8.8-slim
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
    -d leapsight/bondy:0.8.8
```

## Configuring a Bondy node

The methods explained above do not allow you to provide a custom `bondy.conf` file and associated files as explained in the [Configuration Reference](../configuring/configuration-reference/) section.

To learn how to configure Bondy when deploying using Docker read the section [Configuring Bondy on Docker](../configuring/configuring-bondy-on-docker.md).



