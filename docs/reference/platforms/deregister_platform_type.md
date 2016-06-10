---
layout: default
title: Deregister a platform type
---

To deregister a platform type a JSON message of the following form is sent to the local Edgware node:

| Field  | Value                      | Description |
| ------ | -------------------------- | ----------- |
| `op`   | `deregister:platform-type` | Identifies a platform type deregistration message. |
| `type` | \<platform-type>           | The type of the platform to be deregistered. |

The `deregister:platform-type` message may also include the following optional field:
 
| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `correl` | \<correlation-id> | Client-defined correlation ID, present if a status response is required. |

#### Example   

	{
		"op" : "deregister:platform-type",
		"type" : "<platform-type>",
		"correl" : "<correlation-id>" 
	}
    
