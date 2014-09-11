---
layout: default
title: Deregister a user
---

To deregister a user, a JSON message of the following form is sent to the local Edgware node:

| Field  | Value             | Description |
| ------ | ----------------- | ----------- | 
| `op`   | `deregister:user` | Identifies a user deregistration message.
| `id`   | \<user-id>        | The ID of the user to be deregistered.

The `deregister:user` message may also include the following optional field:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `correl` | \<correlation-id> | Client-defined correlation ID, present if a status response is required. |

####Example   

	{
		"op" : "deregister:user",
		"id" : "<user-id>"
	}
