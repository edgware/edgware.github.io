---
layout: default
title: Register a platform
---

Edgware platforms are individually addressable entities on the service bus, distinct from nodes. Specifically, a platform can, at different times in its lifecycle, connect to different Edgware nodes. Since systems connect to platforms, and platforms connect to nodes, platforms provide a layer of indirection between the physical topology (the network of nodes) and the logical set of systems overlaid upon it.

To register a new platform (or a connection to a new node for an exisiting platform) a JSON message of the following form is sent to the local Edgware node:

| Field  | Value                | Description |
| ------ | -------------------- | ----------- | 
| `op`   | `register:platform`  | Identifies a platform registration message. |
| `id`   | \<platform-id>       | The ID of the platform to be registered. |
| `type` | \<platform-type>     | The type of platform. Platform types are not defined by Edgware. |

The `register:platform` message may also include the following optional fields:

| Field    | Value                   | Description |
| -------- | ------------------------| ----------- | 
| `loc`    | \<platform-location>    |  The current geographic location of the platform. This is a JSON object of the form `{"lat" : a, "long" : b, "alt" : c}` where a, b and c are all floating point values. |
| `desc`   | \<platform-description> |  A free text description of the plaform. |
| `attr`   | \<platform-attributes>  |  A set of attributes associated with the platform. This is a JSON object of the form `{"name" : <value>, ... }`. |
| `correl` | \<correlation-id>       |  Client-defined correlation ID, present if a status response is required. |

####Example   

	{
		"op" : "register:platform",
		"id" : "<platform-id>",
		"type" : "<platform-type>",
		"loc" : { "lat" : <latitude>, "long" : <longitude>, "alt" : <altitude> },
		"desc" : "<platform-description>"
		"attr" : "<platform-attributes>"
		"correl" : "<correlation-id>"    
	}
    
