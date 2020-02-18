# Security Basics

## Terminology

* **Authentication** is the process of identifying a user.
* **Authorization** is verifying whether a user has access to perform the requested operation.
* **Groups** can have permissions assigned to them, but cannot be authenticated.
* **Users** can be authenticated and authorized; permissions \(authorization\) may be granted directly or via group membership.
* **Sources** are used to define authentication mechanisms. A user cannot be authenticated to Riak until a source is defined.

## Enabling Security

{% tabs %}
{% tab title="CURL" %}
```bash
curl -X "PUT" "http://localhost:18081/realms/com.myapp.realm/security_enabled" \
     -H 'Content-Type: application/json; charset=utf-8' \
     -H 'Accept: application/json; charset=utf-8'


```
{% endtab %}

{% tab title="WAMP" %}

{% endtab %}
{% endtabs %}

## Disabling Security

{% tabs %}
{% tab title="CURL" %}
```bash
curl -X "DELETE" "http://localhost:18081/realms/com.myapp.realm/security_enabled" \
     -H 'Content-Type: application/json; charset=utf-8' \
     -H 'Accept: application/json; charset=utf-8'
```
{% endtab %}

{% tab title="WAMP" %}

{% endtab %}
{% endtabs %}



