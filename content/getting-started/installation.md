---
title: Installation
weight: 12
menu:
  main:
    parent: Getting Started
    identifier: Installation
    weight: 12
---

## Manual Installation
See the [download page](https://uchiwa.io/#download) to download the packages.

## Debian/Ubuntu

Install the GPG public key:
```sh
wget -q https://sensu.global.ssl.fastly.net/apt/pubkey.gpg -O- | sudo apt-key add -
```

Determine the codename of the Ubuntu/Debian release on your system:
```sh
. /etc/os-release && echo $VERSION
"14.04.4 LTS, Trusty Tahr" # codename for this system is "trusty"
```

Create an APT configuration file at `/etc/apt/sources.list.d/sensu.list`:
```sh
export CODENAME=your_release_codename_here # e.g. "trusty"
echo "deb     https://sensu.global.ssl.fastly.net/apt $CODENAME main" | sudo tee /etc/apt/sources.list.d/sensu.list
```

Update APT:
```sh
sudo apt-get update
```

Install Uchiwa:
```sh
sudo apt-get install uchiwa
```

## RHEL/CentOS

Create the YUM repository configuration file for the Sensu Core repository at `/etc/yum.repos.d/sensu.repo`:
```sh
echo '[sensu]
name=sensu
baseurl=https://sensu.global.ssl.fastly.net/yum/$releasever/$basearch/
gpgcheck=0
enabled=1' | sudo tee /etc/yum.repos.d/sensu.repo
```

Install Sensu:
```sh
sudo yum install sensu
```

## Using Configuration Management

Chef: [uchiwa-chef](https://github.com/sensu/uchiwa-chef)  
Puppet: [puppet-uchiwa](https://github.com/Yelp/puppet-uchiwa)  
Ansible: [ansible-uchiwa](https://github.com/queeno/ansible-uchiwa)  
SaltStack: [sensu-formula](https://github.com/saltstack-formulas/sensu-formula)

## Using Docker

Uchiwa comes pre-packaged in a [Docker container](https://hub.docker.com/r/uchiwa/uchiwa/) for easy deployment.

Download the official Uchiwa Docker image:
```sh
docker pull uchiwa/uchiwa
```

Create a folder that will contain the configuration files:
```sh
mkdir ~/uchiwa-config
```

Create and adjust the main configuration file:
```sh
vi ~/uchiwa-config/config.json
```

Start the Docker container:
```sh
docker run -d -p 3000:3000 -v ~/uchiwa-config:/config uchiwa/uchiwa
```

Browse Uchiwa:
```sh
http://localhost:3000
```

## From Source

{{< note title="Note" >}}
This documentation provides instructions for advanced users who want to build
their own packages. Otherwise, we highly recommend to use the system packages
in order to get stable releases and an easier installation experience.
{{< /note >}}

### Prerequisites
* [Go >= 1.6](https://golang.org/doc/install)
* [NodeJS](https://nodejs.org/en/download/package-manager/)

### Backend

Download the source code:
```sh
go get -d github.com/sensu/uchiwa && cd $GOPATH/src/github.com/sensu/uchiwa
```

Build the Uchiwa binary:
```sh
go build -o build/uchiwa . # Build for your current system
GOOS=linux GOARCH=amd64 go build -o build/uchiwa . # Cross Compilation, see Go documentation
```

### Front-end Assets
Install the front-end assets:
```sh
npm install --production # Standard user
npm install --production --unsafe-perm # Root user
```

### Running Uchiwa Locally
Adjust your configuration:
```sh
cp config.json.example config.json
```

Start Uchiwa
```sh
./build/uchiwa
```

### Developping
See the [Contributing documentation]({{< relref "contributing.md" >}}).
