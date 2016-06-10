---
layout: default
title: Querying for systems
---

To query Edgware for the list of available systems, a JSON message of the following form is sent to the local Edgware node:

| Field    | Value                | Description |
| -------- | -------------------- | ----------- | 
| `op`     | `query:systems` | Identifies a system query message. |
| `correl` | \<correlation-id>    | Client-defined correlation ID to identify the response. |

The `query:systems` message may also include the following optional fields:

| Field      | Value                     | Description |
| ---------- | ------------------------- | ----------- | 
| `type`     | \<system-type-id>         | Query for a specific system type. |
| `id`       | \<system-id>              | Query for a specific system ID. |
| `platform` | \<platform-id>            | Query for systems connected to a specific platform. |
| `attr`     | \<system-type-attributes> | Query for specific system type attributes; will match any system type containing these attributes exactly as specified. |
| `loc`      | \<system-location>        | Query for systems within the geographic area specified in a bounding box. This is a JSON object of the form `{"left" : a, "bottom" : b, "top" : c, "right" : d}` where a, b and c are all floating point values. A system’s location is inherited from its corresponding platform. |

If no optional fields are specified then the full list of available systems will be returned. Each optional field can contain a wildcard character ("\*") matching any string. Wildcards can be used alone or with partial text. Omitting an optional field is equivalent to giving it the value "*".

Matching systems are returned in a JSON message of the form:

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
        <td><code>query-result:systems</code></td>
        <td>Identifies a system query result.</td>
    </tr>
    <tr>
        <td><code>correl</code></td>
        <td></td>
        <td>&lt;correlation-id&gt;</td>
        <td>Client-defined correlation ID to identify the response.</td>
    </tr>
    <tr>
        <td colspan="4">For each matching system the following information will be returned:</td>
    </tr>
    <tr>
        <td><code>systems</code></td>
        <td></td>
        <td></td>
        <td>Identifies the list of systems.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>id</code></td>
        <td>&lt;system-id&gt;</td>
        <td>The system ID.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>type</code></td>
        <td>&lt;system-type&gt;</td>
        <td>The system type.</td>
    </tr>
    <tr>
        <td></td>
		<td><code>desc</code></td>
        <td>&lt;system-description&gt;</td>
        <td>The free text description of the system.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>attr</code></td>
        <td>&lt;system-attributes&gt;</td>
        <td>The set of attributes associated with the system.</td>
    </tr>
</table>

#### Example   

A query of the form:

	{
		"op" : "query:systems",
		"correl" : "<correlation-id>",
		"type" : "<system-type>",
		"loc" : "{"left" : a, "bottom" : b, "top" : c, "right" : d}"
	}

Will generate a response of the form:

	{
		"op" : "query-result:systems",
		"correl" : "<correlation-id>",
		"systems" : [
			{
				"id" : "<system-id>",
				"type" "<system-type>",
				"desc" : "<system-description>",
				"attr" : "<system-attributes>"
			}
		]
	}
