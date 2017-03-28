---
title: Authentication
weight: 40
menu:
  main:
    parent: API
    identifier: Authentication
    weight: 40
---

In order to use the Uchiwa API when authentication is enabled, you must provide
an access token with every request.

Remember to keep your access tokens secret and use HTTPS wherever possible.

## Configuring an access token

1. Set the *accessToken* attribute in the appropriate role; see the
[documentation]({{< relref "getting-started/configuration.md#multiple-users" >}}).
2. Restart Uchiwa to apply this change.

## Providing the access token
**In a header**

```
curl -H "Authorization: token TOKEN" https://localhost:3000/events
```

**As a parameter**

```
curl https://localhost:3000/events?token=TOKEN
```
