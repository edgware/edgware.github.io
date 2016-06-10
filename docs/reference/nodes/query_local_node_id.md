---
layout: default
title: Querying for the local Edgware node ID
---

To query Edgware for the ID of the *local* Edgware node, a JSON message of the following form is sent to the local Edgware node:

| Field    | Value              | Description |
| -------- | ------------------ | ----------- | 
| `op`     | `query:local-node` | Identifies a local node query message. |
| `correl` | \<correlation-id>  | Client-defined correlation ID to identify the response. |

Information about the local node is returned in a JSON message of the form:

| Field    | Value                     | Description |
| -------- | ------------------------- | ----------- | 
| `op`     | `query-result:local-node` | Identifies a local node query result. |
| `correl` | \<correlation-id>         | Client-defined correlation ID to identify the response. |
| `id`     | \<node-id>                | The ID of the local Edgware Node. |

#### Example   

A query of the form:

	{
		"op" : "query:local-node",
		"correl" : "<correlation-id>"
	}
    
Will generate a response in the form:

	{
		"op" : "query-result:local-node",
		"correl" : "<correlation-id>",
    	"id" : "<node-id>"
	}
    
