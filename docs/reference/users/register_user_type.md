---
layout: default
title: Register a user type
---

To register a user type, a JSON message of the following form is sent to the local Edgware node:

| Field  | Value                | Description |
| ------ | -------------------- | ----------- | 
| `op`   | `register:user-type` | Identifies a user type registration message. |
| `type` | \<user-type>         | The type the user type to be registered. |

The `register:user-type` message may also include the following optional fields:

| Field    | Value                    | Description |
| -------- | ------------------------ | ----------- | 
| `desc`   | \<user-type-description> | A free text description of the user type. |
| `attr`   | \<user-type-attributes>  | A set of attributes associated with the user type. This is a JSON object of the form `{"name" : <value>, ... }`. |
| `correl` | \<correlation-id>        | Client-defined correlation ID, present if a status response is required. |

####Example   

	{
		"op" : "register:user-type",
		"type" : "<user-type>"
	}
