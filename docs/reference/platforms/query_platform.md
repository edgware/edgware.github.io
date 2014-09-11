---
layout: default
title: Querying for platforms
---

To query Edgware for the list of platforms connected to the bus, a JSON message of the following form is sent to the local Edgware node:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `op`     | `query:platform`  | Identifies a platform query message. |
| `correl` | \<correlation-id> | Client-defined correlation ID to identify the response. |

The `query:platform` message may also include the following optional fields:
 
| Field    | Value                | Description |
| -------- | -------------------- | ----------- |
| `type`   | \<platform-type>     | Query for a specific platform type. |
| `id`     | \<platform-id>       | Query for a specific platform ID. |
| `attr`   | \<system-attributes> | Query for specific platform attributes; will match any platform containing these attributes exactly as specified. |
| `loc`    | \<system-location>   | Query for platforms within the geographic area specified in a bounding box of the form `{"left" : a, "bottom" : b, "top" : c, "right" : d}`. | 

Matching platforms are returned in a JSON message of the form:

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
        <td><code>query-result:platforms</code></td>
        <td>Identifies a platform query result.</td>
    </tr>
    <tr>
        <td><code>correl</code></td>
        <td></td>
        <td>&lt;correlation-id&gt;</td>
        <td>Client-defined correlation ID to identify the response.</td>
    </tr>
    <tr>
        <td colspan="4">For each matching platform the following information will be returned:</td>
    </tr>
    <tr>
        <td><code>platforms</code></td>
        <td></td>
        <td></td>
        <td>Identifies the list of platforms.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>id</code></td>
        <td>&lt;platform-id&gt;</td>
        <td>The platform ID.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>type</code></td>
        <td>&lt;platform-type&gt;</td>
        <td>The type of the platform.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>loc</code></td>
        <td>&lt;platform-location&gt;</td>
        <td>The current geographic location of the platform.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>desc</code></td>
        <td>&lt;platform-description&gt;</td>
        <td>The free text description of the platform.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>attr</code></td>
        <td>&lt;platform-attributes&gt;</td>
        <td>The set of attributes associated with the platform.</td>
    </tr>
</table>

####Example   

A query of the form:

	{
		"op" : "query:platforms",
		"correl" : "<correlation-id>",
		"type" : "<platform-type>",
		"loc" : {"left" : a,  "bottom" : b, "top" : c,  "right" : d}"
	}
    
Will generate a response in the form:

	{
		"op" : "query-result:platforms",
		"correl" : "<correlation-id>",
		"platforms" : [
			{
				"id" : "<platform-id>",
				"type" "<platform-type>",
				"loc" "<platform-location>",
				"desc" : "<platform-description>",
				"attr" : "<platform-attributes>"
			}
		]
	}
