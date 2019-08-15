---
description: A guide covering commonly adjusted parameters when setting up a new cluster.
---

# Basic Configuration

{% hint style="info" %}
This section covers the parameters that are commonly adjusted when setting up a new cluster. We recommend that you also review the detailed [Configuration Reference](configuration-reference.md) section before moving a cluster into production.
{% endhint %}

All configuration values discussed here are managed via a configuration file on each node, and in most cases a node must be restarted for any changes to take effect.

## Security Settings

To get started we need to define at least one Realm. We recommend to disable security to get started until you get to know how to configure the security subsystem. You can achieve that by creating a Security configuration file and letting Bondy know its location via the `bondy.conf` file. Alternatively you can use the REST API to create the [Realm](../operating/security/realms.md).

{% tabs %}
{% tab title="Configuration Files" %}
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
security.config_file = /bondy/etc/security_conf.json
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endtab %}

{% tab title="REST API" %}
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
{% endtabs %}

## Erlang VM Settings

## Storage Settings

