# mops language

## Overview

mops is a logic-less domain-specific language used by the API Gateway Specification and the Broker Bridge Specification data structures for data transformation and dynamic configuration.

To understand how mops is used in those use cases let's first explore a very simple and non-Bondy related example to understand how mops works.

For the sake of simplicity \(and because Bondy configuration files use JSON\) we will use JSON to represent our data structures in the example.

Let's say we have a Customer Order object we want to transform in a number of ways before we send it to someone else.

```javascript
{
    "id" : 12345
    "sku" : "ZPK1972",
    "price" : 13.99,
    "customer": {
        "first_name": "John",
        "last_name": "Doe",
        "email" : "john.doe@foo.com"
    },
    "ship_to": {
        "first_name": "May",
        "last_name": "Poppins",
        "address" : "3 High Street",
        "town" : "Guildford",
        "county" : "Surrey",
        "zip"   : "GU1 1AF"
    },
    "bill_to": {
        "first_name": "John",
        "last_name": "Doe",
        "address" : "13 Sandy Lane",
        "town" : "Esher",
        "county" : "Surrey",
        "zip"   : "KT11 2PQ"
    }
}
```

mop works by expanding keys \(or key paths\) provided in a context object and adding or updating keys in the same context object. 

In our case we are going to _initialise_ the context object to be the Customer Order.

Let's explore a some example mops expressions to demonstrate how you can use mops in Bondy's configuration objects.

| Expression | Evaluates to |
| :--- | :--- |
| `{{sku}}` | "ZPK1972" |
| `{{customer.first_name}}` | "John" |
| `{{sku |> to_string}}` | "13.99" |
| `{{\"{{customer.firstname}} {{customer.last_name}}\"}}` | "John Doe" |
| `{{\"The sku number is {{sku}}\"}}` | "The sku number is ZPK1972" |



