## Configuration File

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

## Configuration Directories

*Available in Uchiwa 0.14.0 and later*

In addition to the configuration file above, you can provide the location of configuration directories (comma delimited) with the `-d` command line argument.

The Uchiwa packages create the `/etc/sensu/dashboard.d/` directory, which is used by the init script to load additional configuration snippets.

## Configuration Load Order

Uchiwa loads configuration from these sources in the following order:

1. Uchiwa loads configuration from the configuration file (by default, this is located at `/etc/sensu/uchiwa.json` which is provided with the `-c` command line argument).
2. Uchiwa loads configuration snippets from configuration files located in one or multiple Uchiwa configuration directories (by default, this is the `/etc/sensu/dashboard.d/` directory which is provided with the `-d` command line argument).

**Example**

If Uchiwa is started as follows:

```
/opt/uchiwa/bin/uchiwa -c /etc/sensu/uchiwa.json -d /etc/sensu/dashboard.d
```

With the file **/etc/sensu/uchiwa.json**:
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

And the configuration snipppet **/etc/sensu/dashboard.d/site2.json**:
```
{
  "sensu": [
    {
      "name": "Site 2",
      "host": "api2.example.com",
      "port": 4567
    }
  ],
  "uchiwa": {
    "host": "192.168.0.1"
  }
}
```

The resulting loaded configuration will be:
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
      "host": "api2.example.com",
      "port": 4567
    }
  ],
  "uchiwa": {
    "host": "192.168.0.1",
    "port": 3000
  }
}
```
