---
layout: default
title: Prereqs
---   

To run Edgware please ensure that you meet the prereqs listed below.

###Operating system

Edgware has been developed and tested on Windows, Linux, and OS X. Specifically, the following versions have been tested however other distros/versions are likely to work if all other prereqs are met:

**Windows**

* ​Windows 7
* Windows Server 2008
* Windows Server 2012

**Linux**

* ​Ubuntu: 12.04, 14.04
* Fedora: 20
* Red Hat Enterprise Linux (RHEL): 5, 6
* SUSE Linux Enterprise Server (SLES): 11
* Raspbian

**OS X**

* ​OS X 10.9.4

###Prerequisite software

Edgware has two software prereqs:

* **Java:** a Java 2 Standard Edition (J2SE) Java Runtime Environment (JRE) is required to run the Fabric. To develop Fabric extensions a J2SE Java Development Kit (JDK) is also required. The tested version for both the JRE and the JDK is 7.x.
* **Mosquitto broker:** Edgware can be configured for a variety of MQTT-compatable brokers, however out-of-the-box it will work with the [Mosquitto](http://mosquitto.org) open source message broker. You can get the latest version for your system (including Raspberry Pi) from [http://mosquitto.org/download](http://mosquitto.org/download).

Both of these must be available on your system before installing Edgware.

