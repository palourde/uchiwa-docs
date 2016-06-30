### With Packages

Each package contains the Uchiwa binary along with the static HTML and JavaScript files, installed under `/opt/uchiwa`. A sysvinit script is also placed at `/etc/init.d/uchiwa`. The Uchiwa process will be ran under the `uchiwa` user and logs are sent to the files `/var/log/uchiwa.err` and `/var/log/uchiwa.log`.

**Using Configuration Management tools**  
Chef: [uchiwa-chef](https://github.com/sensu/uchiwa-chef)  
Puppet: [puppet-uchiwa](https://github.com/Yelp/puppet-uchiwa)  
Ansible: [ansible-uchiwa](https://github.com/queeno/ansible-uchiwa)  
SaltStack: [sensu-formula](https://github.com/saltstack-formulas/sensu-formula)

**Using Sensu repositories**  
See [Sensu documentation](http://sensuapp.org/docs/latest/dashboards_uchiwa#packages)

**Using HTTP downloads**  
See the [download page](https://uchiwa.io/#download)

### From Source

It's recommended to use the Uchiwa packages in order to ensure the simplest installation process and promote consistency across installations. Otherwise, running from the source code will always be possible.

**Prerequisites**  

* Recent version of git
* Recent version of node
* Recent version of npm ([guide](https://github.com/joyent/node/wiki/installing-node.js-via-package-manager))
* Recent version of go (>= 1.3) ([guide](https://golang.org/doc/install))

**Installation**

* Make sure to set the **GOPATH** environment variable (e.g. `mkdir $HOME/go && export GOPATH=$HOME/go`)
* Also add the workspace's *bin* subdirectory to your PATH: `export PATH=$PATH:$GOPATH/bin`
* Install [Godep](https://github.com/tools/godep): `go get github.com/tools/godep`
* Checkout the source: `go get -d github.com/sensu/uchiwa && cd $GOPATH/src/github.com/sensu/uchiwa`
* Install third-party libraries:  
Under standard user: `npm install --production`  
Under root user: `npm install --production --unsafe-perm`  
* Copy **config.json.example** to **config.json** - modify your Sensu API information. See configuration section.
* Start the dashboard: `godep go run uchiwa.go`
* Open your browser: `http://localhost:3000/`

### With Docker

Uchiwa also comes pre-packaged in a docker container for easy deployment. Make a config.json file for the application, and then launch the uchiwa container with the config mounted as a volume.

* Install Uchiwa from the source (see above)
* Create a folder that will be mount as a volume to the Docker container: `mkdir ~/uchiwa-config`
* Copy your uchiwa config into this last folder: `cp ~/uchiwa/config.json ~/uchiwa-config/config.json`
* Start the Docker container: `docker run -d -p 3000:3000 -v ~/uchiwa-config:/config uchiwa/uchiwa`
