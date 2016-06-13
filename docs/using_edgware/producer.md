---
layout: default
title: Sharing information on the bus
---

Platforms, systems and services that produce information all need to be registered with the bus before they can be used. This is necessary so that they can be discovered by the other apps that need to use them. The details of how to do this can be found in the documentation however we have some predefined types available to us to get started.

Note that registration only needs to be done once. The information will persist in the Edgware Registry until it is either explicitly deleted or the Registry is re-initialised. If Edgware is being used with a pre-configured system then registration might be done as part of the installation process.

Whilst this page focuses on a producer of information, Edgware systems will often be both producers and consumers. The *system type* defines that a system has inputs, outputs or both.

### Register a platform

In this example we'll show the JSON messages that need to be sent to the local Edgware node to create a new system that pushes temperature readings onto the bus. The first step is to tell Edgware that it has a new platform by sending a JSON message of the form:

	{
		"op" : "register:platform",
		"id" : "my_sensor_platform",
		"type" : "sensor",
		"correl" : "101"
	}

Where:

* `op` indicates the operation to be performed by this message, in this case registering a new platform.
* `id` is our own name for the platform.
* `type` gives a type to the platform. Here we use the built-in type `sensor`.
* `correl` is a correlation ID. When we receive a response from Edgware related to this message it will contain this same correlation ID.

### Register a system

Our platform needs to have one or more systems for it to be useful:

	{
		"op" : "register:system",
		"id" : "my_sensor_platform/temp_sensor",
		"type" : "simple_system",
		"correl" : "102"
	}

Where:

* `op` indicates that we are registering a new system.
* `id` is our own name for the system. Whilst platform names must be globally unique, system names only need to be unique within a platform. As such the full name of our system, i.e. the name that we can use any where on Edgware to refer to it, is `platform-name/system-name`, in this case `my_sensor_platform/temp_sensor`.
* `type` gives a type to the system. Here we use the built-in type `simple_system`. Normally we would have also registered our own system type that defines the set of services that we are going to provide.
* `correl` is a correlation ID.

### Activate the system

Having defined our system we can now activate it. This is an important step that tells Edgware that the system is ready for use:

	{
		"op" : "state:system",
		"id" : "my_sensor_platform/temp_sensor",
		"state" : "running",
		"correl" : "103"
	}

Where:

* `op` indicates that we are changing the run-state of the system.
* `id` is the name of the system.
* `state` is the new state of the system; we are starting it so the new state is `running`.
* `correl` is a correlation ID.

### Publish data

We've registered our system, started it, and so we're now ready to start publishing data.

Each system type will define a set of input and output services. Those services that are *output-feeds* are used to publish data onto the bus ready for any consumes that subscribe.

In this example we're going to publish temperature readings onto the bus, using a simple message of the form:

	{
		"op" : "publish",
		"output-feed" : "my_sensor_platform/temp_sensor/untyped_output_feed",
		"msg" : "37.0",
		"correl" : "104"
	}

Where:

* `op` indicates that we are publishing a message onto the bus.
* `output-feed` is the name of the system service that is the originator of the message. Here we use the service `untyped_output_feed` which is predefined for us as part of the `simple_system` system used used above.
* `msg` is the payload of our message.
* `correl` is a correlation ID.

We can now continue to publish temperature readings onto the bus as often as is required. They will be delivered to all of the consumers that have requested them by Edgware.

### Cleaning up

Once we're ready to finish up -- for example when our app is being closed, or our device is being switched off -- we tell Edgware to stop our system using the message:

	{
		"op" : "state:system",
		"id" : "my_app_platform/temp_dashboard",
		"state" : "stopped",
		"correl" : "105"
	}

Where:

* `op` indicates that we are changing the run-state of the system.
* `id` is the name of the system.
* `state` is the new state of the system; we are stopping it so the new state is `stopped`.
* `correl` is a correlation ID.

Edgware will automatically notify any subscribers that the system has now been stopped.
