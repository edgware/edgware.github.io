---
layout: default
title: System and service registration
---

Before a system and its associated services can be used they must be registered in the Edgware Registry. This informaton is used by the Edgware to manage the infrastructure, and to make capabilites discoverable by other systems.

[Register a system](#System)

[Register a system type](#System_type)

[Register a service type](#Service_type)

### <a id="System"></a>Register a system

To register a new system, a JSON message of the following form is sent to the local Edgware node:

| Field  | Value              | Description |
|------- | ------------------ | ----------- |
| `op`   | `register:system`  | Identifies a system registration message. |
| `id`   | \<system-id>       | The ID of the system to be registered. This is the fully qualified, globally unique name of the system, of the form: \<platform-id>/\<system-id>. |
| `type` | \<system-type>     | The type of the system. System types are not defined by Edgware. |

The `register:system` message may also include the following optional fields:
 
| Field    | Value                 | Description |
| -------- | --------------------- | ----------- | 
| `user`   | \<user-id>            | The user ID for this system. Omitting this field will give the system the default user ID (`default`). |
| `desc`   | \<system-description> | A free text description of the system. |
| `attr`   | \<system-attributes>  | A set of attributes associated with the system. This is a JSON object of the form `{"name" : <value>, ... }`. |
| `correl` | \<correlation-id>     | Client-defined correlation ID. Present if a status response is required. |

####Example   

	{
		"op" : "register:system",
    	"id" : "<platform-id>/<system-id>",
    	"type" : "<system-type>",
    	"desc" : "<system-description>",
    	"attr" : "<system-attributes>",
    	"correl" : "<correlation-id>"
    }

### <a id="System_type"></a>Register a system type

To register a new system type, a JSON message of the following form is sent to the local Edgware node:

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
        <td><code>register:system-type</code></td>
        <td>Identifies a system type registration message.</td>
    </tr>
    <tr>
        <td><code>type</code></td>
        <td></td>
        <td>&lt;service-type&gt;</td>
        <td>The system type to be registered.</td>
    </tr>
    <tr>
        <td colspan="4">Each system type must define one or more services using the following fields:</td>
    </tr>
    <tr>
        <td><code>services</code></td>
        <td></td>
        <td></td>
        <td>Identifies the list of services for this system type.</td>
    </tr>
    <tr>
        <td rowspan="4"></td>
        <td><code>type</code></td>
        <td>&lt;service-type id&gt;</td>
        <td>The service type.</td>
    </tr>
    <tr>
        <td colspan="3">The following optional fields can be used to register additional information about each service:</td>
    </tr>
    <tr>
        <td><code>desc</code></td>
        <td>&lt;service-description&gt;</td>
        <td>A free text description of the service.</td>
    </tr>
    <tr>
        <td><code>attr</code></td>
        <td>&lt;service-attributes&gt;</td>
        <td>A set of attributes associated with the service. Service attributes are not defined by Edgware.</td>
    </tr>
    <tr>
        <td colspan="4">An extended form of this message is available to register additional information about the system type using the following optional fields:</td>
    </tr>
    <tr>
        <td><code>desc</code></td>
        <td></td>
        <td>&lt;system-type-description&gt;</td>
        <td>A free text description of the system type.</td>
    </tr>
    <tr>
        <td><code>attr</code></td>
        <td></td>
        <td>&lt;system-type-attributes&gt;</td>
        <td>A set of attributes associated with the system type. System type attributes are not defined by Edgware.</td>
    </tr>
    <tr>
        <td><code>correl</code></td>
        <td></td>
        <td>&lt;correlation­‐id&gt;</td>
        <td>Client-defined correlation ID, present if a status response is required</td>
    </tr>
</table>

####Example   

    {
		"op" : "register:system-type",
    	"type" : "<system-type>",
    	"services" : [
    		{
    			"type" : "<service-type>",
    			"desc" : "<service-type-description>",
    			"attr" : "<service-type-attributes>"
    		}
    	]
    	"desc" : "<system-type-description>",
    	"attr" : "<system-type-attributes>",
    	"correl" : "<correlation-id>"
    }

### <a id="Service_type"></a>Register a service type

To register a new service type, a JSON message of the following form is sent to the local Edgware node:

| Field   | Value                   | Description |
| ------- | ----------------------- | ------------- 
| `op`    | `register:service-type` | Identifies a service type registration message. |
| `id`    | \<service-type>         | The service type to be registered. |
| `mode`  | \<service-mode>         | The mode of the service type, one of `input-feed`, `output-feed`, `notification`, `listener`, `solicit-response` or `request-response`.

The `register:service-type` message may also include the following optional fields:
 
| Field    | Value                       | Description |
| -------- | --------------------------- | ------------- 
| `schema` | \<service-type-schema>      | The schema describing messages accepted or produced by this service type. Service type schemas are not defined by Edgware. |
| `desc`   | \<service-type-description> | A free text descripton of the service type. |
| `attr`   | \<service-type-attributes>  | A set of attributes associated with the service type. This is a JSON object of the form `{"name" : <value>, ... }`. |
| `correl` | \<correlation-id>           | Client-defined correlation ID, present if a status response is required. |

####Example   

	{
		"op" : "register:service-type",
		"type" : "<service-type>",
		"mode" : "<service-mode>",
		"schema" : "<service-type-schema>",
		"desc" : "<service-type-description>",
		"attr" : "<service-type-attributes>",
		"correl" : "<correlation-id>"
	}
