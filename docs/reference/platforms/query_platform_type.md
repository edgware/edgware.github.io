---
layout: default
title: Querying for platform types
---

To query Edgware for the list of platform types, a JSON message of the following form is sent to the local Edgware node:

| Field    | Value                  | Description
| -------- | ---------------------- | ------------- 
| `op`     | `query:platform-types` | Identifies a platform type query message. |
| `correl` | \<correlation-id>      | Client-defined correlation ID to identify the response. |

The `query:platform-types` message may also include the following optional fields:
 
| Field    | Value                       | Description |
| -------- | --------------------------- | ----------- |
| `type`   | \<platform-type>            | Query for a specific platform type. |
| `attr`   | \<platform-type-attributes> | Query for specific platform type attributes; will match any platform type containing these attributes exactly as specified. |

If no optional fields are specified then the full list of available plaform types will be returned. Each optional field can contain a wildcard character ("\*") matching any string. Wildcards can be used alone or with partial text. Omitting an optional field is be equivalent to giving it the value "\*".

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
        <td><code>query-result:platform-types</code></td>
        <td>Identifies a platform type query result.</td>
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
        <td><code>platform-types</code></td>
        <td></td>
        <td></td>
        <td>Identifies the list of platform types.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>type</code></td>
        <td>&lt;platform-type&gt;</td>
        <td>The platform type ID.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>desc</code></td>
        <td>&lt;platform-description&gt;</td>
        <td>The free text description of the platform type.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>attr</code></td>
        <td>&lt;platform-attributes&gt;</td>
        <td>The set of attributes associated with the platform type.</td>
    </tr>
</table>

#### Example   

	{
		"op" : "query:platform-types",
		"correl" : "<correlation-id>",
		"type" : "<platform-type>"
	}
    
Will generate a response in the form:

	{
		"op" : "query-result:platform-types",
		"correl" : "<correlation-id>",
		"platform-types" : [
			{
				"type" "<platform-type>",
				"desc" : "<platform-type-description>",
				"attr" : "<platform-type-attributes>"
			}
		]
	}
