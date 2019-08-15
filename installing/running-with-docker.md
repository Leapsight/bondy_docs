---
description: Bondy is available as a Docker image.
---

# Running with Docker

{% hint style="info" %}
Bondy Docker images are defined in  [bondy\_docker](https://gitlab.com/leapsight/bondy_docker) git repository and the images are published in [Docker Hub](https://hub.docker.com/r/leapsight/bondy).
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

Bondy Docker images are hosted in [Docker Hub](https://hub.docker.com/r/leapsight/bondy).

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

## Customising a Bondy node using Docker

The methods explained above do not allow you to provide a custom `bondy.conf` file and associated files as explained in the [Configuration Reference](../configuring/untitled/configuration-reference.md) section.

In order to do that you will need to create your own docker image. For example:

{% code-tabs %}
{% code-tabs-item title="Dockerfile" %}
```text
FROM leapsight/bondy:0.8.6 AS builder

COPY --chown=bondy:bondy etc/security_config.json /bondy/etc/security_config.json
COPY --chown=bondy:bondy etc/bondy.conf /bondy/etc/bondy.conf

```
{% endcode-tabs-item %}
{% endcode-tabs %}

Lines 3 and 4 of the Dockerfile copy two configuration files from your custom image directory to `/bondy/etc/` directory.

You can find this example in the official docker [repository](https://gitlab.com/leapsight/bondy_docker/tree/master/examples/custom_config).

### OS Environment Variable substitution

The chances are that if you are deploying Bondy using Docker and a Container Orchestration platform like Kubernetes you will need to get some of the configuration values from OS environment variables.

Bondy Docker allows you to define those variables using `${VariableName}` unix shell convention, as shown in the following example.

{% code-tabs %}
{% code-tabs-item title="bondy.conf" %}
```text
nodename = ${BONDY_NODENAME}
distributed_cookie = ${BONDY_COOKIE}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Using the example above, the only modification required for Bondy Docker to substitute those variables with the OS environment counterparts is to add a `.template` extension to every configuration file containing variables. 

{% code-tabs %}
{% code-tabs-item title="Dockerfile" %}
```text
FROM leapsight/bondy:0.8.6 AS builder

COPY --chown=bondy:bondy etc/security_config.json /bondy/etc/security_config.json.template
COPY --chown=bondy:bondy etc/bondy.conf /bondy/etc/bondy.conf.template
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Bondy Docker Image will make the substitution automatically and place the resulting files in the same directory with the `.template` extension removed before calling the `bondy` executable.

{% hint style="danger" %}
Variable substitution will fail if the environment does not have a value set for a variable found in the `.template` files. This will cause the Docker image to fail.
{% endhint %}



