---
layout: default
title: Querying for a user
---

To query Edgware for the list of users connected to the bus, a JSON message of the following form is sent to the local Edgware node:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `op`     | `query:users`     | Identifies a user query message. |
| `correl` | \<correlation-id> | Client-defined correlation ID to identify the response. |

The `query:users` message may also include the following optional fields:

| Field    | Value               | Description |
| -------- | ------------------- | ----------- | 
| `type`   | \<user-type>        | Query for a specific user type. |
| `id`     | \<user-id>          | Query for a specific user ID. |
| `affil`  | \<user-affiliation> | Query for a specific user affiliation. |
| `attr`   | \<user-attributes>  | Query for specific user attributes; will match any user containing these attributes exactly as specified. |

If no optional fields are specified then the full list of registered user will be returned. Each optional field can contain a wildcard character ("\*") matching any string. Wildcards can be used alone or with partial text. Omiting an optional field is equivalent to giving it the value "*".

Matching users are returned in a JSON message of the form:

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
        <td><code>query-result:users</code></td>
        <td>Identifies a user query result.</td>
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
        <td><code>users</code></td>
        <td></td>
        <td></td>
        <td>Identifies the list of users.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>id</code></td>
        <td>&lt;user-id&gt;</td>
        <td>The ID of user.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>type</code></td>
        <td>&lt;user-type&gt;</td>
        <td>The type of the user.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>affil</code></td>
        <td>&lt;user-affiliation&gt;</td>
        <td>The organisational affiliation of the user.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>desc</code></td>
        <td>&lt;user-description&gt;</td>
        <td>The free text description of the user.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>attr</code></td>
        <td>&lt;user-attributes&gt;</td>
        <td>The set of attributes associated with the user.</td>
    </tr>
</table>

####Example   

A query of the form:

	{
		"op" : "query:users",
		"correl" : "<correlation-id>",
	}
    
Will generate a response in the form:

	{
		"op" : "query-result:users",
		"correl" : "<correlation-id>",
		"users" : [
			{
				"id" : "<user-id>",
				"type" "<user-type>",
				"affil" "<user-affiliation>",
				"desc" : "<user-description>",
				"attr" : "<user-attributes>"
			}
		]
	}
