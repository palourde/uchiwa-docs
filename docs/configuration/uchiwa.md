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

**Disable authentication**  
In order to disable Uchiwa authentication, you simply need to remove or leave empty the **user** and **pass** attributes.

### Advanced Authentication

Additional authentication drivers are available within [Sensu Enterprise](http://sensuapp.org/enterprise):

- [GitHub Authentication](features/github)
- [SQL Authentication](features/sql)
