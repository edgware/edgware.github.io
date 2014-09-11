---
layout: default
title: Querying for bearers (networks)
---

To query Edgware for the list of available bearers (networks), a JSON message of the following form is sent to the local Edgware node:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `op`     | `query:bearers`   | Identifies a bearer query message. |
| `correl` | \<correlation-id> | Client-defined correlation ID to identify the response. |

The `query:bearers` message may also include the following optional fields:

| Field       | Value                  | Description |
| ----------- | ---------------------- | ----------- | 
| `id`        | \<bearer-id>           | Query for a specific bearer. |
| `available` | \<bearer-availability> | The availability of the network (bearer), the string `"true"` or `"false"`). |
| `attr`      | \<bearer-attributes>   | Query for specific bearer attributes; will match any bearer containing these attributes exactly as specified. |

If no optional fields are specified then the full list of available bearers will be returned. Each optional field can contain a wildcard character ("\*") matching any string. Wildcards can be used alone or with partial text. Omitting an optional field is equivalent to giving it the value "*".

Matching bearers are returned in a JSON message of the form:

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
        <td><code>query-result:bearers</code></td>
        <td>Identifies a bearer query result.</td>
    </tr>
    <tr>
        <td><code>correl</code></td>
        <td></td>
        <td>&lt;correlation-id&gt;</td>
        <td>Client-defined correlation ID to identify the response.</td>
    </tr>
    <tr>
        <td colspan="4">For each matching bearer the following information will be returned:</td>
    </tr>
    <tr>
        <td><code>bearers</code></td>
        <td></td>
        <td></td>
        <td>Identifies the list of bearers.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>id</code></td>
        <td>&lt;bearer-id&gt;</td>
        <td>The bearer ID.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>available</code></td>
        <td>&lt;bearer-availability&gt;</td>
        <td>The availability of the bearer (the string <code>"true"</code> or <code>"false"</code>).</td>
    </tr>
    <tr>
        <td></td>
        <td><code>desc</code></td>
        <td>&lt;bearer-description&gt;</td>
        <td>The free text description of the bearer.</td>
    <tr>
        <td></td>
        <td><code>attr</code></td>
        <td>&lt;bearer-attributes&gt;</td>
        <td>The set of attributes associated with the bearer.</td>
    </tr>
    </tr>
</table>

####Example   

A query of the form:

	{
		"op" : "query:bearers",
		"correl" : "<correlation-id>"
	}
    
Will generate a response in the form:

	{
		"op" : "query-result:bearers",
		"correl" : "<correlation-id>",
		"bearers" : [
			{
				"id" "<bearer-id>",
				"availability" : "<bearer-availability>",
				"desc" : "<bearer-description>",
				"attr" : "<bearer-attributes>"
			}
    	]
	}
    
