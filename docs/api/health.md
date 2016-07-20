### /health (GET)
Returns both Uchiwa and Sensu API status.

* success: **200 OK**  
```
{
  "uchiwa": "ok",
  "sensu": {
    "0.12.6": {
      "output": "ok"
    },
    "0.13.0":{
      "output": "ok"
    }
  }
}
```
* error: **500 Internal Server Error**  

### /health/sensu (GET)
Returns Sensu status.

* success: **200 OK**  
```
{
  "0.12.6": {
    "output": "ok"
  },
  "0.13.0": {
    "output" :"ok"
  }
}
```
* error: **500 Internal Server Error**  

### /health/uchiwa (GET)
Returns Uchiwa status.

* success: **200 OK**  
```
"ok"
```

* error: **500 Internal Server Error**  
