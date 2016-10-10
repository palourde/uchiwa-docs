---
title: Troubleshooting
weight: 23
menu:
  main:
    parent: Guides
    identifier: Troubleshooting
    weight: 23
---

## Authentication
### How do I disable Uchiwa built-in authentication?
In order to remove Uchiwa authentication, you simply need to remove or
leave empty the **user**, **pass** and **users** attributes from the
[Uchiwa Configuration]({{< relref "getting-started/configuration.md#uchiwa-configuration" >}})
on your configuration file.

## Checks
### My standalone check does not appear in the checks view
Uchiwa uses the **/checks** Sensu API endpoint to build the checks list. This
endpoint only provides the checks that are defined and known by the Sensu server
itself, therefore standalone checks that are only defined on some particular
clients can't be shown. They will, however, appear in the client view since they
are part of the client history.

### Why can't I see the details of a standalone check?
Unless an event is created for this particular check, the details of a
standalone check, such as the command executed, are not available. See the
previous question for more details.

## Errors
### I see the error message *401 Unauthorized*
If you configured a user/pass authentication on your Sensu API, you need to add
these details to your Uchiwa configuration by adding the user and pass attributes
in the proper datacenter object within the *sensu* array, as shown on the
[Datacenters Configuration]({{< relref "getting-started/configuration.md#datacenters-configuration-sensu" >}}).

### I see the error message *x509: certificate signed by unknown authority*
By default, Uchiwa will refuse to make any connection to an API with an invalid
SSL certificate, therefore it needs to be explicitly allowed.
See the **insecure** attribute in the
[Datacenters Configuration]({{< relref "getting-started/configuration.md#datacenters-configuration-sensu" >}}).

## Installation
### Which platforms are supported by Uchiwa?
Uchiwa binaries are compiled for linux, on 386 and amd64 architectures, and
packaged into DEB and RPM packages. If you wish to compile the binary for an
another operating system and compilation architecture,
refer yourself to the
[Installation documentation]({{< relref "getting-started/installation.md#from-source" >}}).
