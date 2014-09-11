---
layout: default
title: Querying for system types
---

To query Edgware for the list of available system types, a JSON message of the following form is sent to the local Edgware node:

| Field    | Value                | Description |
| -------- | -------------------- | ----------- | 
| `op`     | `query:system-types` | Identifies a system type query message. |
| `correl` | \<correlation-id>    | Client-defined correlation ID to identify the response. |

The `query:system-types` message may also include the following optional fields:

| Field       | Value                     | Description |
| ----------- | ------------------------- | ----------- | 
| `type`      | \<system-type-id>         | Query for a specific system type. |
| `attr`      | \<system-type-attributes> | Query for specific system type attributes; will match any system type containing these attributes exactly as specified. |

Additionally, to query for a system type offering *specific service types* the a further set of optional fields may also be included:

| Field      | Nested Field | Value                     | Description |
| ---------- | ------------ | ------------------------- | ----------- | 
| `services` |              |                           | Identifies the list of service types. |
|            | `type`       |\<service-type-id>         | Query for a specific service type. |
|            | `attr`       |\<service-type-attributes> | Query for specific service type attributes; will match any service containing these attributes exactly as specified. |

If no optional fields are specified then the full list of available system types will be returned. Each optional field can contain a wildcard character ("\*") matching any string. Wildcards can be used alone or with partial text. Omitting an optional field is equivalent to giving it the value "*".

Matching system types are returned in a JSON message of the form:

<table>
    <tr>
        <th width="10%">Field</th>
        <th width="10%">Nested Field</th>
        <th width="10%">Nested Field</th>
        <th width="20%">Value</th>
        <th width="50%">Description</th>
    </tr>
    <tr>
        <td><code>op</code></td>
        <td></td>
        <td></td>
        <td><code>query-result:system-types</code></td>
        <td>Identifies a system type query result.</td>
    </tr>
    <tr>
        <td><code>correl</code></td>
        <td></td>
        <td></td>
        <td>&lt;correlation-id&gt;</td>
        <td>Client-defined correlation ID to identify the response.</td>
    </tr>
    <tr>
        <td colspan="5">For each matching system type the following information will be returned:</td>
    </tr>
    <tr>
        <td><code>system-types</code></td>
        <td></td>
        <td></td>
        <td></td>
        <td>Identifies the list of system types.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>type</code></td>
        <td></td>
        <td>&lt;system-type&gt;</td>
        <td>The system type.</td>
    </tr>
    <tr>
         <td></td>
       <td><code>desc</code></td>
        <td></td>
        <td>&lt;system-type-description&gt;</td>
        <td>The free text description of the system type.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>attr</code></td>
        <td></td>
        <td>&lt;system-type-attributes&gt;</td>
        <td>The set of attributes associated with the system type.</td>
    </tr>
    <tr>
        <td></td>
        <td><code>services</code></td>
        <td></td>
        <td></td>
        <td>Identifies a list of services types.</td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td><code>type</code></td>
        <td>&lt;service-type&gt;</td>
        <td>The service type.</td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td><code>desc</code></td>
        <td>&lt;service-type-description&gt;</td>
        <td>The free text description of the service type.</td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td><code>attr</code></td>
        <td>&lt;service-type-attributes&gt;</td>
        <td>The set of attributes associated with the service type.</td>
    </tr>
</table>

####Example   

A query of the form:

	{
		"op" : "query:system-types",
		"correl" : "<correlation-id>",
		"services" : [
			{
				"type" : "<service-type-id>"
			}
		]
	}

Will generate a response of the form:

	{
		"op" : "query-result:system-types",
		"correl" : "<correlation-id>",
		"system-types" : [
			{
				"type" "<system-type-id>",
				"desc" : "<system-description>",
				"attr" : "<system-attributes>",
				"services" : [
					{
						"type" : "<service-type-id>",
						"desc" : "<service-description>",
						"attr" : "<service-attributes>",
					}
				]
			}
		]
	}
