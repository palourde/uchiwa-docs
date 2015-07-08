Uchiwa expose a health API so may easily monitor Uchiwa and the Sensu API endpoints with the **/health** endpoint.

### /health
Returns both Uchiwa and Sensu API status.

* success: **200 OK**  
`{"uchiwa":"ok","sensu":{"0.12.6":{"output":"ok"},"0.13.0":{"output":"ok"}}}`
* error: **500 Internal Server Error**  
`{"uchiwa":"ok","sensu":{"0.12.6":{"output":"connect ECONNREFUSED"},"0.13.0":{"output":"ok"}}}`

### /health/sensu
Returns Sensu status.

* success: **200 OK**  
`{"0.12.6":{"output":"ok"},"0.13.0":{"output":"ok"}}`
* error: **500 Internal Server Error**  
`{"0.12.6":{"output":"connect ECONNREFUSED"},"0.13.0":{"output":"ok"}}`

### /health/uchiwa
Returns Uchiwa status.

* success: **200 OK**  
`"ok"`
* error: **500 Internal Server Error**  
`"error"`
