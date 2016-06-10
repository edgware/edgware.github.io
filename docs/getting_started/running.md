---
layout: default
title: Running Edgware
---   

The Edgware software stack consists of three main components:

* A Java OSGI container to run the services that make up an Edgware *node*
* An Apache Derby database to hold the Edgware *Registry*
* An MQTT-enabled broker used to form the MQTT backbone of the bus

In addition there is an optional Web server supporting the HTTP interface to Edgware.

Each of these components can be started from either the command line or as system services. Using the command line, each component must be started individually via the `fabadmin` command, in the order shown below. To start the components in the background add the `-daemon` command line option.

To start the Edgware components as system services, see the `readme.txt` files under `$FABRIC_HOME/server/linux` or `%FABRIC_HOME%\server\windows`.

**Note:** these instructions assume that the Mosquitto broker is already running, either from the command line or as a system service. Ensure that your Mosquitto broker's configuration matches the sample given in `etc/broker.conf` in the Edgware root directory. See the Mosquitto documentation for more information on configuring your broker.

#### Starting the Registry

	$ fabadmin -s -r <node-name>

*\<node-name\>* is the name that you would like to assign to this Edgware node, and is the name by which it will be known on the bus. It could be, but does not have to be, the host name.

#### Starting the Edgware node

Before you start your node for the first time it is necessary to tell Edgware which network interfaces to use. This is done using the command `fabreg` command:

	fabreg -sn <node-name> fabric.node.interfaces <network-adapter-list>

*\<network-adapter-list\>* is a comma separated list (no spaces) of network adapters e.g. `en0,en5`. Nodes that are associated with multiple adapters will act as gateways between the networks.

The adapter list only needs to be set once (it will be persisted in the Edgware Registry), after which the node can be started:

	$fabadmin -s -n <node-name>

#### Starting the Web server (optional)

	$ fabadmin -s -w

By default you can then access the Edgware Web server at [http://localhost:8080/rest](http://localhost:8080/rest).
