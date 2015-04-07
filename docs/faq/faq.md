# Frequently asked questions

## Authentication

### How do I disable Uchiwa built-in authentication?
In order to remove Uchiwa authentication, you simply need to remove or leave empty the **user** and **pass** attributes from the *uchiwa* object on your configuration file, as shown on the first example [here](configuration/uchiwa/#base).

## Checks

### Why the output of my check is empty?
By design, if your check return the status **0** (success), the output will be discarded by Sensu so there's unfortunately no way to display it in Uchiwa. If you are collecting some kind of metric data, you should consider creating a [Sensu metric check](http://sensuapp.org/docs/latest/adding_a_metric) and add a handler to send it over Graphite, for example.

### My standalone check does not appear in the checks view
Uchiwa uses the **/checks** Sensu API endpoint to build the checks list. This endpoint only provides the checks that are defined and known by the Sensu server itself, therefore standalone checks that are only defined on some particular clients can't be shown. They will, however, appear in the client view since they are part of the client history.

### Why can't I see the details of a standalone check?
Unless an event is created for this particular check, the details of a standalone check, such as the command executed, are not available. See the previous question for more details.

## Datacenters

### What's a datacenter?
Each Sensu API instance is represented, in Uchiwa, by a datacenter. The logic behind it is that you might have an instance in each physical datacenter but nothing prevents you from having multiple Sensu instances within the same physical datacenter, for a development and a production environment.

## Errors

### I see the error message *401 Unauthorized*
If you configured a user/pass authentication on your Sensu API, you need to add these details to your Uchiwa configuration by adding the user and pass attributes in the object of the concerned Sensu array, as shown on the [Sensu settings](configuration/sensu).

### I see the error message *x509: certificate signed by unknown authority*
By default, Uchiwa will refuse to make any connection to an API with an invalid SSL certificate so it needs to be explicitly allowed. See the **insecure** option in the documentation [here](configuration/sensu/).


## Installation

### Which platforms are supported by Uchiwa?

Uchiwa binaries are compiled for linux, on 386 and amd64 architectures, and packaged into DEB and RPM packages. If you wish to compile the binary for an another operating system and compilation architecture, refer yourself to the installation documentation.
