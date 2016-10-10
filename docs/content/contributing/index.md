---
title: Contributing
weight: 50
---

## Installation

### Backend
[Follow these instructions]({{< relref "getting-started/installation.md#from-source" >}})
for the Go backend.

### Frontend
*Optional*. If you wish to modify the frontend components, you'll need to follow
these additional instructions:

Clone the [uchiwa-web](https://github.com/sensu/uchiwa-web) repository:
```sh
git clone git@github.com:sensu/uchiwa-web.git && cd uchiwa-web
```

Install third-party libraries:
```sh
npm install # Standard user
npm install --unsafe-perm # Root user
```

Create a global link for uchiwa-web:
```sh
bower link
```

Move to your uchiwa repository directory:
```sh
cd $GOPATH/src/github.com/sensu/uchiwa
```

Uninstall the uchiwa-web bower component if previously installed:
```sh
bower uninstall uchiwa-web
```

Point the bower component uchiwa-web to the previously created link
```sh
bower link uchiwa-web
```

## Development

### Backend
Run the program:
```sh
go run uchiwa.go
```

**N.B.**: You'll need to relaunch this command if you modify the source code
to apply changes.

### Frontend
Generate **CSS** files from **Sass** templates:
```sh
grunt sass
```

## Testing

### Backend
Run the unit tests:
```sh
go test -v ./...
```

### Frontend
Run linting and unit tests:
```sh
grunt
```
