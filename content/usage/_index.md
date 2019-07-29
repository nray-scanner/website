---
title: "Usage"
weight: 300
pre: <b>3. </b>
---

Nray tries to be easy to understand and use - nevertheless, you may take a few minutes to skim the documentation to understand differences to other scanners.
In contrast to most other port scanners, nray is designed to allow multiple scanning nodes to conduct the scan, therefore achieving better results regarding speed and result accuracy. 
The nray binary can act as *server*, managing all connected nodes, generating work, distributing the scan tasks and collecting results, or, as *node*, perform the hard work delegated by an other nray server instance.

Nearly all configuration is done serverside in a configuration file. 
The are **no** command line flags for most options - config files prevent script wrappers, are easier to read/write, can be kept in source control systems and you can comment them so others understand the rationale behind your configuration. 
If you are new to nray, you may want to start by adopting the configuration file template while looking up configuration options before changing them.

#### Start server

~~~shell
nray server -c </path/to/config.yml>
~~~

#### Start node(s)

~~~shell
nray node -s <server-ip-or-domain-name> -p <port>
~~~