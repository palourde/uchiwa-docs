---
title: High Availability
weight: 21
menu:
  main:
    parent: Guides
    identifier: High Availability
    weight: 21
---

## Datacenters High Availability
You can define multiple Sensu APIs by datacenter in order to provide **failover**
and rudimentary **load balancing** between these APIs.

To get started with this feature, you'll simply need to define at least two
[Sensu objects]({{< relref "getting-started/configuration.md#datacenters-configuration-sensu" >}})
 with the **same name**. Here's a basic example:

```json
{
  "sensu": [
    {
      "name": "us-east-1",
      "host": "10.0.0.1",
      "port": 4567
    },
    {
      "name": "us-east-1",
      "host": "10.0.0.2",
      "port": 4567
    }
  ]  
}
```

With this configuration, the datacenter *us-east-1* now has two APIs (*10.0.0.1* and *10.0.0.2*) and Uchiwa will balance the requests between these two APIs and failback to the second API in case of connectivity issue.



## Uchiwa High Availability
If you are using Uchiwa built-in authentication and wish to run multiple
instances of Uchiwa together, you will need to adjust your configuration.

Uchiwa generates a temporary key during its launch, which is later destroyed once the process is stopped or restarted. This key is used for generating and validating the signatures of the JSON Web Tokens (JWT) for authentication.

This behaviour is problematic when multiple instances of Uchiwa are used behind a load balancer or if the Uchiwa process needs to be frequently restarted. To use your own keys, follow these few steps:

Generate the private key:
```sh
openssl genrsa -out uchiwa.rsa 2048
```

Extract the public key:
```sh
openssl rsa -in uchiwa.rsa -pubout > uchiwa.rsa.pub
```

Adjust the *uchiwa* object in your configuration file in order to specify the path of the keys you just generated:
```json
{
  "uchiwa": {
    "auth": {
      "privatekey": "/path/to/uchiwa.rsa",
      "publickey": "/path/to/uchiwa.rsa.pub"
    }
  }
}
```

Finally, restart Uchiwa and you should see the following entry in your log:
```json
[...]
"message":"Provided RSA keys successfully loaded"
[...]
```
