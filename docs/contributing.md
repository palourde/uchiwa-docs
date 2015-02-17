Everyone is welcome to submit patches. Whether your pull request is a bug fix or introduces new classes or functions to the project, we kindly ask that you include tests for your changes. Even if it's just a small improvement, a test is necessary to ensure the bug is never re-introduced.

### Development Environment

You'll need to install Uchiwa from the source (see the Installation documentation).  

If you want to perform some changes on the web dashboard, you will also need to do the following additional steps:

* Clone the [uchiwa-web](https://github.com/sensu/uchiwa-web) repository: `git clone git@github.com:sensu/uchiwa-web.git && cd uchiwa-web`
* Install third-party libraries:  
Under standard user: `npm install --production`  
Under root user: `npm install --production --unsafe-perm`  
* Create a global link for uchiwa-web: `bower link`
* Move to your uchiwa repository: `cd $GOPATH/src/github.com/sensu/uchiwa`
* Uninstall the uchiwa-web bower component: `bower uninstall uchiwa-web`
* Point the bower componenent uchiwa-web to the previously created link: `bower link uchiwa-web`

### Testing

**uchiwa**  
The command `go test -v ./...` will execute the proper unit tests.

**uchiwa-web**  
In order to install all the tools, please run `npm install`.  
The command `grunt` will execute the proper linting and unit tests.
