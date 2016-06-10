---
layout: default
title: Querying for nodes
---

To query Edgware for the list of nodes connected to the bus, a JSON message of the following form is sent to the local Edgware node:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `op`     | `query:nodes`     |  Identifies a node query message. |
| `correl` | \<correlation-id> | Client-defined correlation ID to identify the response. |

The `query:nodes` message may also include the following optional fields:

| Field     | Value              | Description |
| --------- | ------------------ | ----------- | 
| `id`      | \<node-id>         | Query for a specific node. |
| `address` | \<node-address>    | Query for a node with a specific address (URI). |
| `attr`    | \<node-attributes> | Query for specific node attributes; will match any node containing these attributes exactly as specified. |

If no optional fields are specified then the full list of available nodes will be returned. Each optional field can contain a wildcard character ("\*") matching any string. Wildcards can be used alone or with partial text. Omitting an optional field is equivalent to giving it the value "*".

Matching platform types are returned in a JSON message of the form:

<table>
    <tr>
        <th>Field</th>
        <th>Nested Field</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td><code>op</code></td>
        <td></td>
        <td><code>query-result:nodes</code></td>
        <td>Identifies a node query result.</td>
    </tr>
    <tr>
        <td><code>correl</code></td>
        <td></td>
        <td>&lt;correlation-id&gt;</td>
        <td>Client-defined correlation ID to identify the response.</td>
    </tr>
    <tr>
        <td colspan="4">For each matching node the following information will be returned:</td>
    </tr>
    <tr>
        <td><code>nodes</code></td>
        <td></td>
        <td></td>
        <td>Identifies the list of nodes.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>id</code></td>
        <td>&lt;node-id&gt;</td>
        <td>The node ID.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>address</code></td>
        <td>&lt;node-address&gt;</td>
        <td>The address (URI) of the node.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>desc</code></td>
        <td>&lt;node-description&gt;</td>
        <td>The free text description of the node.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>attr</code></td>
        <td>&lt;node-attributes&gt;</td>
        <td>The set of attributes associated with the node.</td>
    </tr>
</table>

#### Example   

A query of the form:

	{
		"op" : "query:nodes",
		"correl" : "<correlation-id>"
	}
    
Will generate a response in the form:

	{
		"op" : "query-result:nodes",
		"correl" : "<correlation-id>",
		"nodes" : [
			{
				"id" "<node-id>",
				"address" : "<node-address>",
				"desc" : "<node-description>",
				"attr" : "<node-attributes>"
			}
    	]
	}
    
