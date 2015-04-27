The SQL authentication driver is part of [Sensu Enterprise](http://sensuapp.org/enterprise).

This driver is compatible with the following databases:

* MySQL
* PostgreSQL (>= 9.x)
* SQLite

**Configuration**  

A default user, **admin**, will be automatically created with the password **sensu**.

*MySQL*  
You need to create the **DB_NAME** beforehand.
```
{
  "uchiwa": {
    "db": {
      "driver": "mymysql",
      "scheme": "tcp:MYSQL_HOST:MYSQL_PORT*DB_NAME/USERNAME/PASSWORD"
    }
  }
}
```

*PostgreSQL*  
You need to create the **DB_NAME** beforehand.
```
{
  "uchiwa": {
    "db": {
      "driver": "postgres",
      "scheme": "user=USERNAME dbname=DB_NAME host=HOST password=PASSWORD sslmode=disable"
    }
  }
}
```

*SQLite*  

The **FILENAME.db** database file will automatically be created.
```
{
  "uchiwa": {
    "db": {
      "driver": "sqlite3",
      "scheme": "FILENAME.db"
    }
  }
}
```
