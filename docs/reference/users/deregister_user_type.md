---
layout: default
title: Deregister a user type
---

To deregister a user type, a JSON message of the following form is sent to the local Edgware node:

| Field  | Value                  | Description |
| ------ | ---------------------- | ----------- | 
| `op`   | `deregister:user-type` | Identifies a user type deregistration message. |
| `type` | \<user-type>           | The user type to be deregistered. |

The `deregister:user-type` message may also include the following optional field:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `correl` | \<correlation-id> | Client-defined correlation ID, present if a status response is required. |

#### Example   

	{
		"op" : "deregister:user-type",
		"type" : "<user-type>"
	}
    
