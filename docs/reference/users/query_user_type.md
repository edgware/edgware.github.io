---
layout: default
title: Querying for user types
---

To query Edgware for the list of user types, a JSON message of the following form is sent to the local Edgware node:

| Field    | Value              | Description
| -------- | ------------------ | ------------- 
| `op`     | `query:user-types` | Identifies a user type query message. |
| `correl` | \<correlation-id>  | Client-defined correlation ID to identify the response. |

The `query:user-types` message may also include the following optional fields:
 
| Field    | Value                   | Description |
| -------- | ----------------------- | ----------- |
| `type`   | \<user-type>            | Query for a specific user type. |
| `attr`   | \<user-type-attributes> | Query for specific user type attributes; will match any platform type containing these attributes exactly as specified. |

If no optional fields are specified then the full list of available user types will be returned. Each optional field can contain a wildcard character ("\*") matching any string. Wildcards can be used alone or with partial text. Omitting an optional field is be equivalent to giving it the value "\*".

Matching user types are returned in a JSON message of the form:

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
        <td><code>query-result:user-types</code></td>
        <td>Identifies a user type query result.</td>
    </tr>
    <tr>
        <td><code>correl</code></td>
        <td></td>
        <td>&lt;correlation-id&gt;</td>
        <td>Client-defined correlation ID to identify the response.</td>
    </tr>
    <tr>
        <td colspan="4">For each matching platform type the following information will be returned:</td>
    </tr>
    <tr>
        <td><code>user-types</code></td>
        <td></td>
        <td></td>
        <td>Identifies the list of user types.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>type</code></td>
        <td>&lt;user-type&gt;</td>
        <td>The user type.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>desc</code></td>
        <td>&lt;user-type-description&gt;</td>
        <td>The free text description of the user type.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>attr</code></td>
        <td>&lt;user-type-attributes&gt;</td>
        <td>The set of attributes associated with the user type.</td>
    </tr>
</table>

####Example   

	{
		"op" : "query:user-types",
		"correl" : "<correlation-id>",
	}
    
Will generate a response in the form:

	{
		"op" : "query-result:user-types",
		"correl" : "<correlation-id>",
		"user-types" : [
			{
				"type" "<user-type>",
				"desc" : "<user-type-description>",
				"attr" : "<user-type-attributes>"
			}
		]
    }
