# Configuring Bondy on Docker

In order to configure Bondy when using Docker you will have two options: 

1. [Mounting a volume with the config files](configuring-bondy-on-docker.md#mounting-a-volume-with-the-config-files) when executing the `docker run` command 
2. [Creating your own docker image](configuring-bondy-on-docker.md#creating-your-own-docker-image) based on the official images

## **Mounting a volume with the config files**

First, you will need to create your config files in a local directory e.g. `~/tmp/bondy/etc` and map it to the `bondy/etc` directory exposed by the docker image.

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

## Creating your own docker image

Another way to configure Bondy which might allow for further DevOps customisation is to create your own custom docker image from the official images. 

The following example shows how to do it.

{% code-tabs %}
{% code-tabs-item title="Dockerfile" %}
```text
FROM leapsight/bondy:0.8.6 AS builder

COPY etc/security_config.json /bondy/etc/security_config.json
COPY etc/bondy.conf /bondy/etc/bondy.conf

```
{% endcode-tabs-item %}
{% endcode-tabs %}

Lines `3` and `4` copy two configuration files from your custom image subdirectory`/etc`  to the `/bondy/etc/` directory. 

You can find this example in the official docker [repository](https://gitlab.com/leapsight/bondy_docker/tree/master/examples/custom_config).

{% hint style="info" %}
### OS Environment Variable substitution

The chances are that if you are deploying Bondy using Docker and a Container Orchestration platform like Kubernetes you will need to get some of the configuration values from OS environment variables.

Bondy Docker image allows you to define those variables using `${VariableName}` unix shell convention, as shown in the following example.

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

Bondy Docker image will make the substitution automatically and place the resulting files in the same directory with the `.template` extension removed before calling the `bondy` executable.

Variable substitution will fail if the environment does not have a value set for a variable found in the `.template` files. This will cause the Docker image to fail.
{% endhint %}

