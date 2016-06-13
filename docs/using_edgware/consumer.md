---
layout: default
title: Consuming information from the bus
---

Platforms, systems and services that consume information all need to be registered with the bus before they can be used. This is necessary so that they can be discovered by the other apps that need to use them. The details of how to do this can be found in the documentation however we have some predefined types available to us to get started.

Note that registration only needs to be done once. The information will persist in the Edgware Registry until it is either explicitly deleted or the Registry is re-initialised. If Edgware is being used with a pre-configured system then registration might be done as part of the installation process.

Whilst this page focuses on a consumer of information, Edgware systems will often be both producers and consumers. The *system type* defines that a system has inputs, outputs or both.

### Register a platform

In this example we'll show the JSON messages that need to be sent to the local Edgware node to create a new system that consumes temperature readings from the bus. The first step is to tell Edgware that it has a new platform by sending a JSON message of the form:

	{
		"op" : "register:platform",
		"id" : "my_app_platform",
		"type" : "app",
		"correl" : "201"
	}

Where:

* `op` indicates the operation to be performed by this message, in this case registering a new platform.
* `id` is our own name for the platform.
* `type` gives a type to the platform. Here we use the built-in type `app`.
* `correl` is a correlation ID. When we receive a response from Edgware related to this message it will contain this same correlation ID.

### Register a system

Our platform needs to have one or more systems for it to be useful:

	{
		"op" : "register:system",
		"id" : "my_app_platform/temp_dashboard",
		"type" : "simple_system",
		"correl" : "202"
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
		"id" : "my_app_platform/temp_dashboard",
		"state" : "running",
		"correl" : "203"
	}

Where:

* `op` indicates that we are changing the run-state of the system.
* `id` is the name of the system.
* `state` is the new state of the system; we are starting it so the new state is `running`.
* `correl` is a correlation ID.

### Subscribe to data from another system

We've registered our system, started it, and so we're now ready to start consuming data.

Each system type will define a set of input and output services. Those services that are *input-feeds* are used to receive data from the bus.

In this example we're going to consume the temperature readings pushed onto the bus by our [producer](producer.html) example, using a simple message of the form:

	{
		"op" : "subscribe",
		"output-feeds" : ["*/temp_sensor/*"],
		"input-feed" : "my_app_platform/temp_dashboard/untyped_input_feed",
		"correl" : "204"
	}

Where:

* `op` indicates that we are subscribing to data from the bus.
* `output-feeds` indicates a list of patterns against which we want to match our subscription. In this case we want to subscribe to all data feeds from systems called `temp_sensor` on any platform.
* `input-feed` is the name of one of our own system services (defined in the system type) to which we want the data delivered. If our pattern matches multiple output-feed services then all of the messages that they produce will be delivered to this input-feed. Here we use the service `untyped_input_feed` which is predefined for us as part of the `simple_system` system used used above.
* `correl` is a correlation ID.

Edgware will tell us which output-feeds on the bus have matched our subscription with a response message of the form:

	{
		"op" : "subscriptions",
		"output-feeds" : ["my_sensor_platform/temp_sensor/untyped_output_feed"],
		"input-feed" : "my_app_platform/temp_dashboard/untyped_input_feed",
		"correl" : "204"
	}

Where:

* `op` indicates that this is a list of active subscriptions.
* `output-feeds` indicates a list of actual output-feeds that matched the pattern in our subscription message. The data from these feeds will be delivered to us across the bus.
* `input-feed` is the name of the input-feed system service to which we asked for the data feeds to be delivered.
* `correl` is a correlation ID.

### Delivery of data feed messages

We are now ready to receive temperature readings from the bus. When one is published it will arrive in a message of the form:

	{
		"op" : "feed-message",
		"output-feed" : "my_sensor_platform/temp_sensor/untyped_output_feed",
		"msg" : "37.0",
		"input-feed" : "my_app_platform/temp_dashboard/untyped_input_feed",
		"encoding":"ascii"
	}

Where:

* `op` indicates that this is a data feed message from one of the output-feeds to which we have subscribed.
* `output-feed` is the name of the output-feed system service that produced the message. In this case it is the [producer](producer.html) that we have defined.
* `msg` is the payload of the message.
* `input-feed` is the name of the input-feed system service to which we asked for the data feed to be delivered.
* `encoding` is the encoding of the message data. The default is `ascii`.

Our app can now process this information as needed.

### Unsubscribing from one or more output feeds

We can selectively unsubscribe from one or more of out active subscriptions. The following example will unsubscribe from all output-feeds associated with the input feed `my_app_platform/temp_dashboard/untyped_input_feed`:

	{
		"op" : "unsubscribe",
		"input-feed" : "my_app_platform/temp_dashboard/untyped_input_feed",
		"correl" : "205"
	}

Where:

* `op` indicates that this is an unsubscribe request.
* `input-feed` is the name of the input-feed system service for which we want to cancel the subscriptions.
* `correl` is a correlation ID.

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

Edgware will automatically cancel any active subscriptions as part of stopping the system.
