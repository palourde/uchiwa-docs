### Base

The *uchiwa* object can contain the following attributes:

```
"uchiwa": {
  "host": "0.0.0.0",
  "port": 3000,
  "refresh": 5
}
```

**host**  
*String*. Address on which Uchiwa will listen. The default value is **0.0.0.0**.

**port**  
*Integer*. Port on which Uchiwa will listen. The default value is **3000**.

**refresh**  
*Integer*. Determines the interval to pull the Sensu APIs, in seconds. The default value is **5**.

### Simple authentication
In order to restrict the access to the dashboard, you can easily setup a single-user account with these attributes:

```
"uchiwa": {
  [...]
  "user": "admin",
  "pass": "secret"
}
```

**user**  
*String*. Username of the Uchiwa dashboard.

**pass**  
*String*. Password of the Uchiwa dashboard.

### SQL authentication
The SQL authentication module is part of [Sensu Enterprise](http://sensuapp.org/enterprise).

The module contains the following database drivers:

* MySQL
* PostgreSQL (>= 9.x)
* SQLite

**Configuration**  

A default user, **admin**, will be automatically created with the password **uchiwa**.

*MySQL*  
You need to create the **DB_NAME** beforehand.
```
"uchiwa": {
  [...]
  "db": {
    "driver": "mymysql",
    "scheme": "tcp:MYSQL_PORT:MYSQL_PORT*DB_NAME/USERNAME/PASSWORD"
  },
}
```

*PostgreSQL*  
You need to create the **DB_NAME** beforehand.
```
"uchiwa": {
  [...]
  "db": {
    "driver": "postgres",
    "scheme": "user=USERNAME dbname=DB_NAME host=HOST password=PASSWORD sslmode=disable"
  },
}
```

*SQLite*  

The **FILENAME.db** database file will automatically be created.
```
"uchiwa": {
  [...]
  "db": {
    "driver": "sqlite3",
    "scheme": "FILENAME.db"
  },
}
```
