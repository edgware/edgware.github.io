---
layout: default
title: Deregister a platform
---

To deregister a platform a JSON message of the following form is sent to the local Edgware node:

| Field    | Value                 | Description |
| -------- | --------------------- | ----------- |
| `op`     | `deregister:platform` | Identifies a platform deregistration message. |
| `id`     | \<platform-id>        | The ID of the platform to be deregistered. |

The `deregister:platform` message may also include the following optional field:
 
| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `correl` | \<correlation-id> | Client-defined correlation ID, present if a status response is required. |

####Example   

	{
		"op" : "deregister:platform",
		"id" : "<platform-id>",
		"correl" : "<correlation-id>"   
	}
    
