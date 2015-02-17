The *sensu* array contains an object for every Sensu API, represented as **datacenter** in Uchiwa.

Each object can contain the following attributes:

```
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
```
**name**  
*String*. Name of the Sensu API (used as datacenter name). If empty, a random one will be generated.

**host**  
*String*. Hostname or IP address of the Sensu API. **Required**.

**port**  
*Integer*. Port of the Sensu API. The default value is **4567**.

**ssl**  
*Boolean*. Determines whether or not to use the HTTPS protocol. The default value is **false**.

**insecure**  
*Boolean*. Determines whether or not to accept an insecure SSL certificate. The default value is **false**.

**path**  
*String*. Path of the Sensu API. Leave empty in case of doubt.

**timeout**  
*Integer*. Timeout for the Sensu API, in seconds. The default value is **5**.

**user**  
*String*. Username of the Sensu API. Leave empty for none.

**pass**  
*String*. Password of the Sensu API. Leave empty for none.
