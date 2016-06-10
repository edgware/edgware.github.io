---
layout: default
title: Deregister a node
---

To deregister a node as a neighbour of the local Edgware node, a JSON message of the following form is sent to the local Edgware node:

| Field | Value             | Description |
| ----- | ----------------- | ----------- | 
| `op`  | `deregister:node` | Identifies a node deregistration message. |
| `id`  | \<node-id>        | The ID of the node to be deregistered. |

The `deregister:node` message may also include the following optional field:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `correl` | \<correlation-id> | Client-defined correlation ID, present if a status response is required.

#### Example   

	{
		"op" : "deregister:node",
		"id" : "<node-id>"
	}
    
