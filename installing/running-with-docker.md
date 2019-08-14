---
description: Bondy is available as a Docker image.
---

# Running with Docker

## Run a Bondy node using docker

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

Bondy Docker images are hosted in [Docker Hub](https://hub.docker.com/r/leapsight/bondy).

```bash
docker run --name bondy_1 -d leapsight/bondy:master
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

In case you need to expose them or want to configure port mapping you would run it like this:

```bash
docker run \
    -p 18080:18080 \
    -p 18081:18081 \
    -p 18082:18082 \
    -p 18086:18086 \
    --name bondy1 \
    -d leapsight/bondy:0.8.6
```

## Customising Bondy when deployed using Docker

The methods explained above do not allow you to provide a custom `bondy.conf` file as explained in the [Configuration Reference](../configuring/untitled/configuration-reference.md) section.

In order to do that you will need to create your own docker image. For example:

```bash
FROM leapsight/bondy:develop AS builder

COPY --chown=bondy:bondy etc/security_config.json /bondy/etc/security_config.json
COPY --chown=bondy:bondy etc/bondy.conf /bondy/etc/bondy.conf

```

You can find this example in the official docker [repository](https://gitlab.com/leapsight/bondy_docker/tree/master/examples/custom_config).

### OS Environment Variable substitution

The chances are that if you are deploying Bondy using Docker and a Container Orchestration platform like Kubernetes you will need to get some of the configuration values from OS environment variables from within the configuration files.

```text
nodename = ${BONDY_NODENAME}
distributed_cookie = ${BONDY_COOKIE}
```

For this kind of situation, the Bondy Docker image provides a way of replacing those variables with their OS environment variables counterparts.

Using the example above, the only modification required is to add a `.template` extension to those configuration files containing variables and Bondy will make the substitution automatically before calling the `bondy` executable.

```bash
FROM leapsight/bondy:develop AS builder

COPY --chown=bondy:bondy etc/security_config.json /bondy/etc/security_config.json.template
COPY --chown=bondy:bondy etc/bondy.conf /bondy/etc/bondy.conf.template
```

{% hint style="danger" %}
Variable substitution will fail if the environment does not have a value set for a variable found in the `.template` files. This will cause the Docker image to fail.
{% endhint %}

## Additional tools for contributors

If you need to build an image locally you can use the following make targets with the provided Makefile.

```text
make develop
```

```text
make develop-slim
```

In case you need to change the bondy configuration files, you can follow the examples in the examples folder.

There is even a target for that.

```text
make example-custom-config
```

Once you build your iamge you would run it like this:

```bash
docker run \
    -p 18080:18080 \
    -p 18081:18081 \
    -p 18082:18082 \
    -p 18086:18086 \
    --name bondy-example-custom-config \
    -d example-custom-config
```

