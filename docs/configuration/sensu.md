### Base

The *sensu* array contains an object for every Sensu API, represented as **datacenters** in Uchiwa.

Each object can contain the following attributes:

```
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
**name** (required)  
*String*.
Name of the Sensu API (used as datacenter name). If empty, a random one will be generated.

**host** (required)  
*String*.  
Hostname or IP address of the Sensu API.

**port**  
*Integer*.  
Port of the Sensu API. The default value is `4567`.

**ssl**  
*Boolean*.  
Determines whether or not to use the HTTPS protocol. The default value is `false`.

**insecure**  
*Boolean*.  
Determines whether or not to accept an insecure SSL certificate. The default value is `false`.

**path**  
*String*.  
Path of the Sensu API.

**timeout**  
*Integer*.  
Timeout for the Sensu API, in seconds. The default value is `5`.

**user**  
*String*.  
Username of the Sensu API.

**pass**  
*String*.  
Password of the Sensu API.

### Datacenters High Availability

Starting with Uchiwa **0.13.0**, you can now define multiple Sensu APIs by datacenter in order to provide **failover** and rudimentary **load balancing** between these APIs.

To get started with this feature, you'll simply need to define at least two Sensu APIs with the same **name**. Here's a basic example:

```
{
  "sensu": [
    {
      "name": "us-east-1",
      "host": "10.73.0.100",
      "port": 4567
    },
    {
      "name": "us-east-1",
      "host": "10.73.0.202",
      "port": 4567
    }
  ]  
}

```

With this configuration, the datacenter *us-east-1* now has two APIs (*10.73.0.100* and *10.73.0.202*) and Uchiwa will balance the requests between these two APIs and failback to the other API in case of connectivity issue.
