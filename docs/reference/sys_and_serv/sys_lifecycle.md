---
layout: default
title: System lifecycle management
---

The run-time lifecycle of a system is indicated via one of two states: *running* and *stopped*. A newly registered system is initially in the stopped state, and it is only when the system is running that it will be operational. The system itself will manage the transiton between the states:

stopped ➔ running ➔ stopped

informing its local Edgware node at each transiton.

A system is not required to explicitly subscribe to receive messages from its input‐feed, listener, and request-response services. Edgware will perform this operaton automatcally when the system enters the running state; Edgware will also unsubscribe on behalf of the system when it enters the stopped state. Edgware will not pass any messages to the system until all of these subscriptions have been initialised. A system can choose to receive a message from Edgware indicating when this is the case.

### Changing the state of a system

To set the state of a system, a JSON message of the following form is sent to the local Edgware node:

| Field   | Value           | Description |
| ------- | --------------- | ----------- | 
| `op`    | `status:system` | Identifies a state change request message. |
| `id`    | \<system-id>    | The ID of the system for which the state is being changed. This is the fully qualified, globally unique name of the system, of the form: \<platform-id>/\<system-id> |
| `state` | \<new-state>    | The system's new state, one of `running` or `stopped`. |

The `register:system` message may also include the following optional field:
 
| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `correl` | \<correlation-id> | Client-defined correlation ID, present if a status response is required. |

If a correlation ID has been provided then Edgware will respond with a message indicating the result of the state change request:

| Field    | Value                 | Description
| -------- | --------------------- | ------------- 
| `op`     | `state-change:system` | Identifies a state change response message. |
| `id`     | \<system-id>          | The ID of the system for which the state has changed. This is the fully qualified, globally unique name of the system, of the form:  \<platform-id>/\<system-id> |
| `state`  | \<new-state>          | The new state of the system, one of `running`, indicting that each of the system's subscriptions has been initialised and it will begin to receive messages, or `stopped`, indicating that each of the system's subscriptions has been terminated and it will no longer receive messages. |
| `correl` | \<correlation-id>     |  Client-defined correlation ID identifying the response. |

####Example

    {
    	"op" : "state:system",
    	"id" : "<platform-id>/<system-id>",
    	"state" : "<new-state>",
    	"correl" : "<correlation-id>"
    }

Once the state change has been actioned Edgware will (if requested) send an acknowledgement of the form:

	{
		"op" : "state-change:system",
		"id" : "<platform-id>/<system-id>",
		"state" : "<new-state>",
		"correl" : "<correlation-id>"
	}
