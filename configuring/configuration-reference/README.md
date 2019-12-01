# Configuration Reference

## The `bondy.conf` file

Bondy  has a `bondy.conf` configuration file that is used to set a wide variety of _static configuration options_ for Bondy and its location depends on the type of install you are using shown in the following table.

| Install Type | bondy.conf location |
| :--- | :--- |
| Source install | `/etc` |
| Docker Image | `/bondy/etc` |

The `bondy.conf` file is used to set a wide variety of configuration options for Bondy. The file uses a sysctl-like syntax that looks like this:

{% code title="bondy.conf" %}
```text
nodename = bondy@127.0.0.1
distributed_cookie = bondy
security.allow_anonymous_user = off
```
{% endcode %}

{% hint style="warning" %}
Notice that for every option not provided by your configuration, Bondy will define a default value \(also specified in the following sections\).
{% endhint %}

### Variables

Within the `bondy.conf` file you can use the following variables which Bondy will substitute before running.

| Variable | Description |
| :--- | :--- |
| `platform_etc_dir` |  |

The following is an example of how to use variable substitution.

{% code title="bondy.conf" %}
```bash
broker_bridge.config_file = $(platform_etc_dir)/broker_bridge_config.json
```
{% endcode %}

{% hint style="warning" %}
Notice these mechanism cannot be used to do OS environment variables substitution.   
However, Bondy provides a tool for OS variable substitution that is automatically used by the Bondy Docker image start script. To understand how to use OS environment variables substitution in Docker read [this](../configuring-bondy-on-docker.md#os-environment-variable-substitution) section, otherwise take a look at how the `start.sh` script uses it in the official docker images.
{% endhint %}

## Feature-specific configuration files

Some features and/or subsystems in Bondy  allow providing an additional JSON configuration file e.g. the Security subsystem.

In those cases, we need to let Bondy know where to find those specific files. This is done in the `bondy.conf` under the desired section e.g. the following configuration file adds the location for the `security_conf.json` file.

{% code title="bondy.conf" %}
```text
nodename = bondy@127.0.0.1
distributed_cookie = bondy
security.allow_anonymous_user = off
security.config_file = /bondy/etc/security_conf.json
```
{% endcode %}

\*\*\*\*

## Advance configuration options

In addition to the `bondy.conf` file , you can place a `vm.args` configuration file in the same path in which you find `bondy.conf` to configure Bondy's Erlang VM.

{% hint style="danger" %}
Notice that providing your own`vm.args` works differently than providing a `bondy.conf` file. While your `bondy.conf` options are merged with the defaults, thus overriding the defaults for the keys you provide but leaving intact the others, the `vm.args` options are a full replacement of the dynamically generated `vm.args` by Bondy. 

So only use this option if you really know what you are doing. If you really need to do this, we suggest  using Bondy's generated `vm.args` as a base for your customisations.
{% endhint %}

