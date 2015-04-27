The Uchiwa packages install the configuration file at `/etc/sensu/uchiwa.json`.

This configuration file must contains [sensu](configuration/sensu) object, which defines all Sensu APIs and the [uchiwa](configuration/uchiwa) object, which specifies the dashboard settings.

**Minimal Configuration**
```
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

**Complete Configuration**
```
{
    "sensu": [
      {
        "name": "Site 1",
        "host": "api1.example.com",
        "port": 4567
      },
      {
        "name": "Site 2",
        "host": "127.0.0.1",
        "port": 443,
        "ssl": true,
        "insecure": true,
        "path": "/site2",
        "timeout": 5,
        "user": "admin",
        "pass": "secret"
      }
    ],
    "uchiwa": {
      "host": "0.0.0.0",
      "port": 3000,
      "refresh": 5,
      "user": "admin",
      "pass": "secret"
    }
  }
```
