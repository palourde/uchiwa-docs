The GitHub authentication driver is part of [Sensu Enterprise](http://sensuapp.org/enterprise). This driver is compatible with **github.com**.

**Register an OAuth Application in GitHub**

* Log into GitHub
* Visit the application page under your organization's settings and click on **Register a new OAuth Application**.
![github_app](img/github_app.png)
* The most important setting is the **Authorization callback URL**. This URL only needs to be accessible by **your users**, therefore it can be an internal URL within your private network. You must use the following format: `{DASHBOARD_URL}/login/callback`.
* Once you created the application, note down the **Client ID** and the **Client Secret**.
![github_app](img/github_secret.png)

**Dashboard Configuration**

```
{
  "uchiwa": {
    "github": {
      "clientId": "a8e43af034e7f2608780",
      "clientSecret": "b63968394be6ed2edb61c93847ee792f31bf6216",
      "roles": {
        "guests": [
          "myorganization/devs"
        ],
        "operators": [
          "myorganization/owners"
        ]
      },
      "server": "https://github.com"
    }
  }
}
```

**clientId** (required)  
*String*.  
The **Client ID** generated in the previous step.

**clientSecret** (required)  
*String*.  
The **Client Secret** generated in the previous step.

**roles** (required)  
*Object*.  
Contains any or all of the **guests** and **operators** arrays, which contain strings in the format of `organization_name/team_name`

**server** (required)  
*String*.  
URL of the GitHub server.
