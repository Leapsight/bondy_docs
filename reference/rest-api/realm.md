# Security

## Realms

{% api-method method="get" host="http://localhost:18081" path="/realms/" %}
{% api-method-summary %}
List all realms
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to retrieve all realms.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Accept" type="string" required=true %}
application/json; charset=utf-8
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
    {
        "authmethods": [
            "wampcra",
            "ticket",
            "anonymous"
        ],
        "description": "A test realm",
        "uri": "com.leapsight.test"
    },
    {
        "authmethods": [
            "wampcra",
            "ticket"
        ],
        "description": "The Bondy administrative realm.",
        "uri": "com.leapsight.bondy"
    }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="http://localhost:18081" path="/realms" %}
{% api-method-summary %}
Add a realm
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Users

## Groups

## Sources

## Grants

