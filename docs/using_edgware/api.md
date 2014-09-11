---
layout: default
title: Edgware API
---
A lightweight JSON interface is provided for Edgware services and apps, i.e. producers and consumers of information. For simplicity we'll use the term app to cover anything that connects to Edgware.

Apps send JSON messages Edgware and receive responses using one of two protocols:

1. MQTT: messages are published to a single input topic on the app's local broker, and response messages and notifications returned with a corresponding output topic.
2. Web sockets: messages are sent to and received from Edgware using a Web sockets connection to the built-in Web server.

### MQTT

A client can interact with Edgware by sending and receiving JSON messages to the broker running on its local Edgware node. Two broker topics are used for this interaction:

**Inbound topic**

This is the topic used to send messages to the Edgware node; i.e. the client will publish to this topic.

	$fabric/<node-id>/$adapters/$mqtt/$in/<client-id>
	
Where:

* `<node-id>` is the name of the local Edgware node.
* `<client-id>` is the MQTT client ID used to connect to the broker.

**Outbound topic**

This is the topic used by Edgware to return responses and send other messages to the client; i.e. the client will subscribe to this topic.

	$fabric/<node-id>/$adapters/$mqtt/$out/<client-id>
	
Where:

* `<node-id>` is the name of the local Edgware node.
* `<client-id>` is the MQTT client ID used to connect to the broker.

**Will message**

When connecting to the broker the client should also specify the following will message, which will ensure that the client's connection to Edgware is properly terminated if it should disconnect:

	{
		"op" : "disconnect",
		"client-id" : "<client-id>"
	}

Where:

* `op` indicates that this is a disconnection message.
* `<client-id>` is the same client ID used in the inbound and outbound topics above.

The topic for the will message is the inbound topic.

### Web sockets

An example of how to used the Web sockets interface is included in the source code. See the project fabric.tools.rest.
