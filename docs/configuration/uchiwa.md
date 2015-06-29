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
Starting with Uchiwa **0.10.0**, you can now define multiple users within your configuration file. The **users** attribute  have precedence over the **user** attribute.

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
