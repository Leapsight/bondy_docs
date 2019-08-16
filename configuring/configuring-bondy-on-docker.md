# Configuring Bondy on Docker

In order to configure Bondy when running on Docker you will need to create your own docker image. For example:

{% code-tabs %}
{% code-tabs-item title="Dockerfile" %}
```text
FROM leapsight/bondy:0.8.6 AS builder

COPY etc/security_config.json /bondy/etc/security_config.json
COPY etc/bondy.conf /bondy/etc/bondy.conf

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

COPY etc/security_config.json /bondy/etc/security_config.json.template
COPY etc/bondy.conf /bondy/etc/bondy.conf.template
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Bondy Docker Image will make the substitution automatically and place the resulting files in the same directory with the `.template` extension removed before calling the `bondy` executable.

{% hint style="danger" %}
Variable substitution will fail if the environment does not have a value set for a variable found in the `.template` files. This will cause the Docker image to fail.
{% endhint %}

