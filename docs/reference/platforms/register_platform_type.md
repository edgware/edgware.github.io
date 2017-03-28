---
layout: default
title: Register a platform type
---

To register a new platform type, a JSON message of the following form is sent to the local Edgware node:

| Field  | Value                    | Description |
| ------ | ------------------------ | ----------- | 
| `op`   | `register:platform-type` | Identifies a platform type registration message. |
| `type` | \<platform-type>         | The platform type to be registered. |

The `register:platform-type` message may also include the following optional fields:

| Field    | Value                        | Description |
| -------- | ---------------------------- | ----------- | 
| `desc`   | \<platform-type-description> |  A free text description of the platform type. |
| `attr`   | \<platform-type-attributes>  |  A set of attributes associated with the platform type. This is a JSON object of the form `{"name" : <value>, ... }`. |
| `correl` | \<correlation-id>            |  Client-defined correlation ID, present if a status response is required. |

#### Example   

	{
		"op" : "register:platform-type",
		"type" : "<platform-type>", 
		"desc" : "<platform-type-description>",
		"correl" : "<correlation-id>"  
	}
    
