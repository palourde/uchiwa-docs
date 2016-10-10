---
title: Security
weight: 22
menu:
  main:
    parent: Guides
    identifier: Security
    weight: 22
---

## Encrypted Passwords
You can place hashed passwords in the *password*
attributes, but only within the **uchiwa** object, in order to obfuscate
users passwords in your configuration files.

Please note that you must **absolutely** use the `{crypt}` prefix when using an encrypted
password. For example:
```
"password": "{crypt}$1$MteWnoFT$yhEi8KMxO794K0TIriZcI0"
```

The following algorithms are supported (along the commands to create the hashes):

Algorithm | Command
----------|---------
APR1 | `openssl passwd -apr1 MY_PASSWORD`
MD5 | `mkpasswd --method=MD5 MY_PASSWORD`
SHA-256 | `mkpasswd --method=SHA-256 MY_PASSWORD`
SHA-512 | `mkpasswd --method=SHA-512 MY_PASSWORD`


## HTTPS Encryption
You can serve all content over HTTPS, using Uchiwa, without the need of
a reverse proxy. To get started, follow these few steps:

*Optional* - Generate a private key:
```sh
openssl genrsa -out uchiwa.key 2048
```

*Optional* - Generate a self-signed certificate:
```sh
openssl req -new -x509 -key uchiwa.key -out uchiwa.pem -days 365
```

Adjust the *uchiwa* object in your configuration file in order to specify the
path of the keys you just generated:
```json
{
  "uchiwa": {
    "ssl": {
      "certfile": "/path/to/uchiwa.pem",
      "keyfile": "/path/to/uchiwa.key"
    }
  }
}
```

Finally, restart Uchiwa and access your dashboard over HTTPS.
