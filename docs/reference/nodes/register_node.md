---
layout: default
title: Register a node
---

To register a node as a neighbour of the local Edgware node, a JSON message of the following form is sent to the local Edgware node:

| Field     | Value           | Description |
| --------- | --------------- | ----------- | 
| `op`      | `register:node` | Identifies a node registration message. |
| `id`      | \<node-id>      | The ID of the node to be registered. |
| `address` | \<node-address> | The address (URI) of how to connect to the node. |

The `register:node` message may also include the following optional fields:

| Field    | Value                   | Description |
| -------- | ----------------------- | ----------- | 
| `desc`   | \<node-description>     | A free text description of the node. |
| `attr`   | \<user-node-attributes> | A set of attributes associated with the node. This is a JSON object of the form `{"name" : <value>, ... }`. |
| `correl` | \<correlation-id>       | Client-defined correlation ID, present if a status response is required. |

####Example   

	{
		"op" : "register:node",
		"id" : "<node-id>",
		"address" : "<node-address>"
	}
    
