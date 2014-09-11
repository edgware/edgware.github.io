---
layout: default
title: System and service deregistration
---

Once a system and its associated services are no longer required then they can be removed from the Edgware Registry.

[Deregister a system](#System)

[Deregister a system type](#System_type)

[Deregister a service type](#Service_type)


### <a id="System"></a>Deregister a system

To deregister a system, a JSON message of the following form is sent to the local Edgware node:

| Field | Value               | Description |
| ----- | ------------------- | ----------- | 
| `op`  | `deregister:system` | Identifies a system deregistration message. |
| `id ` | \<system-id>        | The ID of the system to be redegistered. This is the fully qualified, globally unique name of the system, of the form: \<platform-id>/\<system-id>. |

The `deregister:system` message may also include the following optional field:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- |
| `correl` | \<correlation-id> | Client-defined correlation ID, present if a status response is required. |

The system and its services will no longer be available for use until re-registered.

####Example   

    {
    	"op" : "deregister:system",
    	"id" : "<platform-id>/<system-id>",
		"correl" : "<correlation-id>"
    }

### <a id="System_type"></a>Deregister a system type

To deregister a system type, a JSON message of the following form is sent to the local Edgware node:

| Field | Value                    | Description |
| ----- | ------------------------ | ----------- |
| `op`  | `deregister:system-type` | Identifies a system type deregistration message. |
| `id`  | \<system-id>             | The system type to be redegistered. |

The `deregister:system` message may also include the following optional field:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- |
| `correl` | \<correlation-id> | Client-defined correlation ID, present if a status response is required. |

The system type will only be deregistered if there are no instances of the specified type currently registered.

####Example   

    {
	    "op" : "deregister:system-type",
    	"type" : "<system-type>",
    	"correl" : "<correlation-id>"
    }

### <a id="Service_type"></a>Deregister a service type

To deregister a service type, a JSON message of the following form is sent to the local Edgware node:

| Field | Value                     | Description |
| ----- | ------------------------- | ----------- | 
| `op`  | `deregister:service-type` | Identifies a service type deregistration message. |
| `id`  | \<service-type>           | The service type to be deregistered. |

The `deregister:service-type` message may also include the following optional field:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- |
| `correl` | \<correlation-id> | Client-defined correlation ID, present if a status response is required. |

The service type will only be deregistered if there are no system types using the specified service type currently registered.

####Example   

    {
		"op" : "deregister:service-type",
		"type" : "<service-type>",
		"correl" : "<correlation-id>"
    }
