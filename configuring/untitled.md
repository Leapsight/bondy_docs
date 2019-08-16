---
description: A guide covering commonly adjusted parameters when setting up a new cluster.
---

# Basic Configuration

{% hint style="info" %}
This section covers the parameters that are commonly adjusted when setting up a new cluster. We recommend that you also review the detailed [Configuration Reference](configuration-reference.md) section before moving a cluster into production.
{% endhint %}

All configuration values discussed here are managed via a configuration file on each node, and in most cases a node must be restarted for any changes to take effect.

## The `bondy.conf` file

Bondy  has a `bondy.conf` configuration file that is used to set a wide variety of _static configuration options_ for Bondy and its location depends on the type of install you are using shown in the following table.

| Install Type | bondy.conf location |
| :--- | :--- |
| Source install | `/etc` |
| Docker Image | `/bondy/etc` |

The `bondy.conf` file is used to set a wide variety of configuration options for Bondy. The file uses a sysctl-like syntax that looks like this:

{% code-tabs %}
{% code-tabs-item title="bondy.conf" %}
```text
nodename = bondy@127.0.0.1
distributed_cookie = bondy
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="warning" %}
Notice that for every option not provided by your configuration, Bondy will define a default value \(also specified in the following sections\).
{% endhint %}

## Security Settings

To get started we need to define at least one [WAMP Realm](../operating/security/realms.md). 

{% hint style="info" %}
A Realm is an administrative domain in WAMP, it acts as a namespace for all resources \(users, groups, permissions, procedures and topics\). WAMP is a session-based protocol and all messages are routed only through the session's Realm.
{% endhint %}

To get started we recommend you disable security until you get to know how to configure the security subsystem. For that you need to create a Realm you will connect to, and disable security using the `security_enabled` parameter which accepts the values `on` or `off`which, as you might suspect, map to the boolean values `true` and `false` respectively.

You can achieve this by creating a security configuration file and letting Bondy know its location via the `bondy.conf` file. Alternatively you can use the Admin REST API or the WAMP API to create the realm.

{% tabs %}
{% tab title="Configuration Files" %}
The security configuration file can be named anything you like. The important thing is that \(i\) you give it a name anyone will understand, and \(ii\) that we use the same name on the `bondy.conf` file as shown in the following snippets.

{% code-tabs %}
{% code-tabs-item title="security\_config.json" %}
```javascript
{
  "uri": "com.myapp.test",
  "description": "A test realm",
  "security_enabled" : false
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="bondy.conf" %}
```text
nodename = bondy@127.0.0.1
distributed_cookie = bondy
security.config_file = /bondy/etc/security_conf.json
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endtab %}

{% tab title="Admin REST API" %}
Notice that in the case of the REST API the `security_enabled` parameter takes a JSON`boolean` value.

{% code-tabs %}
{% code-tabs-item title="Create a Realm" %}
```bash
curl -X "POST" "http://localhost:18081/realms/" \
     -H 'Content-Type: application/json; charset=utf-8' \
     -H 'Accept: application/json; charset=utf-8' \
     -d $'{
  "uri": "com.leapsight.test",
  "description": "Test",
  "security_enabled" : false
}'
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endtab %}

{% tab title="WAMP API" %}
To be defined.
{% endtab %}
{% endtabs %}

The [Security Settings](security.md) section provides the details of the Realm resource and the security configuration file format and the supported parameters, but for now the above snippet will suffice to get you going.

{% hint style="warning" %}
#### Static vs Dynamic Configuration

There is a difference between creating a Realm using configuration files \(static configuration\) or the REST or WAMP APIs \(dynamic configuration\). 

The effect of both methods is that a Realm resource is persisted in Bondy's replicated storage, and if part of the cluster, replicated to all nodes. However, the configuration files are re-applied every time a node is restarted, and as a result, you might be replacing any changes that you might have done using the APIs before restart.

We recommend using static configuration for things that might not change during the lifetime of your system e.g. realms, groups and permissions, administrative or infrastructure users, OAuth2 clients.
{% endhint %}

## Erlang VM Settings

## Storage Settings

