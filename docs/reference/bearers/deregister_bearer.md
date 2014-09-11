---
layout: default
title: Deregister a bearer (network)
---

To deregister a new bearer (network), a JSON message of the following form is sent to the local Edgware node:

| Field | Value               | Description |
| ------| ------------------- | ----------- | 
| `op`  | `deregister:bearer` | Identifies a bearer deregistration message. |
| `id`  | \<bearer-id>        | The ID of the bearer to be deregistered. |

The `deregister:bearer` message may also include the following optional fields

| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `correl` | \<correlation-id> | Client-defined correlation ID, present if a status response is required. |

####Example   

	{
		"op" : "deregister:bearer",
		"id" : "<bearer-id>"
	}
    
