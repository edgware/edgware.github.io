---
layout: default
title: Introduction
---

###A service bus for the physical world

Edgware is a lightweight, agile service bus that was developed for M2M solutions. It provides many of the features found in an [enterprise service bus](http://en.wikipedia.org/wiki/Enterprise_service_bus) - discovery, routing, message transformation etc. - but built for resource constrained, dynamic and/or unreliable environments. Edgware integrates systems at the very edge of the network into a [service oriented architecture](http://en.wikipedia.org/wiki/Service-oriented_architecture), running on (or alongside) the devices that it connects.

Since Edgware supports unattended systems it is designed to be self managing. A discovery protocol enables neighbouring nodes to quickly form into a bus that spans the network. Edgware tracks which systems are connected, what services they offer, when they are being used.

New software services can we deployed onto the bus, enabling local processing of information at or near its point of origin, saving valuable network bandwidth and helping manage effectively the large volumes of data that is often captured where the digital world meets the physical world.

###Edgware and MQTT

Edgware has at its core a publish/subscribe message bus that uses the [MQTT](http://mqtt.org/) protocol to move information around.

Publish/subscribe decouples the producers and consumers of information. Edgware extends this principle across a	 network of MQTT-compatible brokers, federating them into a single virtual publish/subscribe platform. Producers and consumers only ever talk to their local brokers, and Edgware does the rest.

###For more information

If you have a question or suggestion, there are various places you can do so:

 - Subscribe to the [mailing list](https://groups.google.com/forum/#!forum/edgware)
   and the [blog](http://blog.edgware-fabric.org)
 - Follow [@edgware](http://twitter.com/edgware-fabric) on Twitter
 - Chat on `#edgware` on `irc.freenode.net`

