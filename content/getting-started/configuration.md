---
title: Configuration
weight: 13
menu:
  main:
    parent: Getting Started
    identifier: Configuration
    weight: 13
---

## Configuration Load Order
Uchiwa loads configuration from these sources in the following order:

1. Uchiwa loads configuration from the configuration file (by default, this is located at `/etc/sensu/uchiwa.json` which is provided with the `-c` command line argument).
2. Uchiwa loads configuration snippets from configuration files located in one or multiple Uchiwa configuration directories (by default, this is the `/etc/sensu/dashboard.d/` directory which is provided with the `-d` command line argument).

## Minimal Configuration

```json
{
  "sensu": [
    {
      "name": "Site 1",
      "host": "api1.example.com",
      "port": 4567
    }
  ],
  "uchiwa": {
    "host": "0.0.0.0",
    "port": 3000
  }
}
```

## Datacenters Configuration (Sensu)
The *sensu* array contains a hash for every Sensu API, represented as **datacenters** in Uchiwa.

Each hash can contain the following attributes:
```json
{
  "sensu": [
    {
      "name": "API Name",
      "host": "127.0.0.1",
      "port": 443,
      "ssl": true,
      "insecure": true,
      "path": "/site2",
      "timeout": 5,
      "user": "admin",
      "pass": "secret"
    }
  ]  
}

```

Key     | Required | Type | Description
--------|----------|------|------
name | false | string | Name of the Sensu API (used as datacenter name). If empty, a random one will be generated.
host | true | string | Hostname or IP address of the Sensu API.
port | false | integer | Port of the Sensu API. The default value is `4567`.
ssl | false | boolean | Determines whether or not to use the HTTPS protocol. The default value is `false`.
insecure | false | boolean | Determines whether or not to accept an insecure SSL certificate. The default value is `false`.
path | false | string | Path of the Sensu API.
timeout | false | integer | Timeout for the Sensu API, in seconds. The default value is `5`.
user | false | string | Username of the Sensu API.
pass | false | string | Password of the Sensu API.

## Uchiwa Configuration

The *uchiwa* hash can contain the following attributes:

```json
{
  "uchiwa": {
    "host": "0.0.0.0",
    "port": 3000,
    "loglevel": "info",
    "refresh": 10,
    "user": "admin",
    "pass": "secret",
    "users": {...},
    "auth": {...},
    "ssl": {...},
    "useroptions": {...}
  }
}
```

Key     | Required | Type | Description
--------|----------|------|------
host | false | string | Address on which Uchiwa will listen. The default value is `0.0.0.0`.
port | false | integer | Port on which Uchiwa will listen. The default value is `3000`.
loglevel | false | string | Level of logging to show after Uchiwa has started. The default value is `info`. Allowed values are `trace`, `debug`, `info`, `warn`, `fatal`
refresh | false | integer | Determines the interval to pull the Sensu APIs, in seconds. The default value is `10`.
user | false | string | Username of the Uchiwa dashboard. Remove to disable authentication.
pass | false | string | Password of the Uchiwa dashboard. Remove to disable authentication.
users | false | hash | [See the Mutliple Users documentation]({{< relref "#multiple-users" >}}). Has precedence over the **user** attribute.
auth | false | hash | [See the High Availability documentation]({{< relref "guides/high-availability.md#uchiwa-high-availability" >}}).
ssl | false | hash | [See the HTTPS Encryption documentation]({{< relref "guides/security.md#https-encryption" >}}).
useroptions | false | hash | [See the User Options documentation]({{< relref "#user-options" >}}).

### Multiple Users

You can define multiple users, including read-only users, within your
users attribute. The **users** attribute has precedence over the **user** attribute.

```json
{
  "uchiwa": {
    "users": [
      {
        "username" : "admin",
        "password": "secret",
        "accessToken": "vFzX6rFDAn3G9ieuZ4ZhN-XrfdRow4Hd5CXXOUZ5NsTw4h3k3l4jAw__",
        "readonly": false
      },
      {
        "username" : "guest",
        "password": "secret",
        "accessToken": "hrKMW3uIt2RGxuMIoXQ-bVp-TL1MP4St5Hap3KAanMxI3OovFV48ww__",
        "readonly": true
      }
    ]
  }
}
```

Key     | Required | Type | Description
--------|----------|------|------
username | true | string | Username of the user.
password | true | string | Password of the user. Also see the [Encrypted Passwords documentation]({{< relref "guides/security.md#encrypted-passwords" >}}).
accessToken | false | string | A unique and secure token to interact with the Uchiwa API as the related user. Remember to keep your access tokens secret. Must only contain friendly URL characters. [See Generating an access token]({{< relref "#generating-an-access-token" >}}).
readonly | false | boolean | Restrict write access to the dashboard (create stashes, delete clients, etc.). The default value is `false`.

### User Options

This hash can set various global user options.

```json
{
  "uchiwa": {
    "useroptions": {
        "disablenoexpiration": false,
        "expireonresolvedefault": true
    }
  }
}
```

Key     | Required | Type | Description
--------|----------|------|------
disablenoexpiration | false | boolean | Disables the `No expiration` option from the silence creation page. The default value is `false`.
expireonresolvedefault | false | boolean | Default value of the `Expire on Resolve` checkbox on the silence creation page. The default value is `false`.

### Generating an access token
An access token must only contain friendly URL characters. We recommend using
the following command to create a proper token:
```
openssl rand -base64 40 |  tr -- '+=/' '-_~'```
```
