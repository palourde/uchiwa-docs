The LDAP authentication driver is part of [Sensu Enterprise](http://sensuapp.org/enterprise).

This driver is tested with **Microsoft Active Directory** (AD) and should be compatible with any LDAP directory.


**Configuration**
```
{
  "uchiwa": {
    "ldap": {
      "server": "localhost",
      "port": 389,
      "basedn": "cn=users,dc=domain,dc=tld",
      "roles": {
        "guests": [
          "guests_group"
        ],
        "operators": [
          "operators_group"
        ]
      },
      "security": "none"
    }
  }
}
```

**server** (required)  
*String*.  
**IP address** or **FQDN** of the LDAP directory or the Microsoft Active Directory domain controller.

**port** (required)  
*Integer*.  
Port of the LDAP/AD service. Usually *389* or *636*.

**basedn** (required)  
*String*.  
Tells which part of the directory tree to search. For example, `cn=users,dc=domain,dc=tld` will search into all *users* of the *domain.tld* directory.

**roles** (required)  
*Object*.  
Contains any or all of the **guests** and **operators** arrays, which contain strings in the format of `group_name`

**security** (required)  
*String*.
Determines the encryption level of the connection to the LDAP server. Possible values are **none**, **starttls** and **tls**.
