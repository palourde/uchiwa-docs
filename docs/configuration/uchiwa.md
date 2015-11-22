### Base

The *uchiwa* object can contain the following attributes:

```
{
  "uchiwa": {
    "host": "0.0.0.0",
    "port": 3000,
    "refresh": 5
  }
}
```

**host**  
*String*.  
Address on which Uchiwa will listen. The default value is **0.0.0.0**.

**port**  
*Integer*.  
Port on which Uchiwa will listen. The default value is **3000**.

**refresh**  
*Integer*.  
Determines the interval to pull the Sensu APIs, in seconds. The default value is **5**.

### Simple Authentication
In order to restrict the access to the dashboard, you can easily setup a single-user account with these attributes:

```
{
  "uchiwa": {
    "user": "admin",
    "pass": "secret"
  }
}
```

**user**  
*String*.  
Username of the Uchiwa dashboard.

**pass**  
*String*.  
Password of the Uchiwa dashboard.

### Multiple users with Simple Authentication
Starting with Uchiwa **0.10.0**, you can now define multiple users, including read-only users, within your configuration file. The **users** attribute has precedence over the **user** attribute.

```
{
  "uchiwa": {
    "users": [
      {
        "username" : "admin",
        "password": "secret",
        "role": {
          "readonly": false
        }
      },
      {
        "username" : "guest",
        "password": "secret",
        "role": {
          "readonly": true
        }
      }
    ]
  }
}
```

**username**  
*String*.  
Username of the account.

**password**  
*String*.  
Password of the account.

**readonly**  
*Boolean*.  
Restrict *write* access to the dashboard (create stashes, delete clients, etc.)

### Disable authentication
In order to disable Uchiwa authentication, you simply need to remove or leave empty the **user** and **pass** attributes.

### Static RSA keys
Starting with Uchiwa **0.13.0**, it's now possible to use your own 2048-bit RSA key. By default, Uchiwa generates a temporary key during its launch, which is later destroyed once the process is stopped or restarted. This key is used for generating and validating the signatures of the JSON Web Tokens (JWT) for the authentication.

This behavior is problematic when multiple instances of Uchiwa are used behind a load balancer or if the Uchiwa process needs to be frequently restarted. To use your own keys, follow these few steps:

Generate the private key:
```
openssl genrsa -out uchiwa.rsa 2048
```

Extract the public key:
```
openssl rsa -in uchiwa.rsa -pubout > uchiwa.rsa.pub
```

Adjust the *uchiwa* object in your configuration file in order to specify the path of the keys you just generated:
```
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
```
[...]"Output":"Provided RSA keys successfully loaded"}
```
