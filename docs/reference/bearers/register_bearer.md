---
layout: default
title: Register a bearer (network)
---

To register a new bearer (network), a JSON message of the following form is sent to the local Edgware node:

| Field          | Value                  | Description |
| -------------- | ---------------------- | ----------- | 
| `op`           | `register:bearer`      | Identifies a bearer (network) registration message. |
| `id`           | \<bearer-id>           | The ID of the bearer (network) to be registered. |
| `availability` | \<bearer-availability> | The availability of the bearer (network), the string `"true"` or `"false"`). |

The `register:bearer` message may also include the following optional fields:

| Field    | Value                 | Description |
| -------- | ----------------------| ----------- | 
| `desc`   | \<bearer-description> | A free text description of the bearer (network).
| `attr`   | \<bearer-attributes>  | A set of attributes associated with the bearer (network). This is a JSON object of the form `{"name" : <value>, ... }`. |
| `correl` | \<correlation-id>     | Client-defined correlation ID, present if a status response is required.

Typical network attributes include:

1. `"bandwidth"`: the bandwidth of link (bytes per second)
2. `"latency"`: the latency of link (milliseconds end-to-end)
3. `"mtu"`: the MTU (Maximum Transmission Unit), i.e. the maximum size of packet before fragmentation occurs.

For example:

		"attr" : {"bandwidth" : 100000000, "latency" : 20, "mtu" : 1500 }   
    
Note that bearers do not need to be unregistered – they can just be marked unavailable.

####Example   

	{
		"op" : "register:bearer",
		"id" : "<bearer-id>",
		"available" : "true",
	}
