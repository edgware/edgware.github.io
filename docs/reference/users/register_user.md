---
layout: default
title: Register a user
---

The users of Edgware are identified by a user ID, which is then associated with one or more running systems. Users can be both producers and consumers of information, and can represent both human users and software/hardware systems. User IDs will often be task IDs associated with a role (for example, "maintenance" or "operator"), but can be unique to a specific individual or entity. They can be used to provide access control, and as part of user-level policy-based management on an Edgware bus.

Before a user ID can be used it must be registered. On Linux or Windows systems a user ID may equate to a user account (login ID), and corresponding credentials, for that particular system. Note that there is a default user ID that will be used for a system if one is not provided explicitly. 

### Register a new user

To register a user, a JSON message of the following form is sent to the local Edgware node:

| Field  | Value           | Description |
| ------ | --------------- | ----------- | 
| `op`   | `register:user` | Identifies a user registration message. |
| `id`   | \<user-id>      | The ID of the user to be registered. |
| `type` | \<user-type>    | The type of the user. User types are not defined by Edgware. |

The `register:user` message may also include the following optional fields:

| Field    | Value               | Description |
| -------- | ------------------- | ----------- | 
| `affil`  | \<user-affiliation> | The organisational affiliation of the user. Organisational affiliations are not defined by Edgware. |
| `desc`   | \<user-description> | A free text description of the user. |
| `attr`   | \<user-attributes>  | A set of attributes associated with the user. This is a JSON object of the form `{"name" : <value>, ... }`. |
| `correl` | \<correlation-id>   | Client-defined correlation ID, present if a status response is required. |

####Example   

	{
		"op" : "register:user",
		"id" : "<user-id>",
		"type" : "<user-type>"
	}
    
