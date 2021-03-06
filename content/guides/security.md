---
title: Security
weight: 23
menu:
  main:
    parent: Guides
    identifier: Security
    weight: 23
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


Alternatively, you could use the [Passlib hashing library for Python 2 & 3]
(https://passlib.readthedocs.io/en/stable/).

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

### TLS Configuration

Additional attributes can be provided to tweak the TLS configuration:
```json
{
  "uchiwa": {
    "ssl": {
      "certfile": "/path/to/uchiwa.pem",
      "keyfile": "/path/to/uchiwa.key",
      "ciphersuite": [
        "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256",
        "TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384",
        "TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305",
        "TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA",
        "TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA",
        "TLS_RSA_WITH_AES_128_GCM_SHA256",
        "TLS_RSA_WITH_AES_256_GCM_SHA384",
        "TLS_RSA_WITH_AES_128_CBC_SHA",
        "TLS_RSA_WITH_AES_256_CBC_SHA",
      ],
      "tlsminversion": "tls10"
    }
  }
}
```

Key     | Required | Type | Description
--------|----------|------|------
ciphersuite | false | array of strings | List of cipher suite supported. See the example above for the default suite. Available cipher suites are listed in the [Go TLS documentation](https://golang.org/src/crypto/tls/cipher_suites.go).
tlsminversion | false | string | Minimum supported version of TLS. Allowed values are `tls10`, `tls11` & `tls12`.
