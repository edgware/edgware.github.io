---
layout: default
title: Request/response
---

A running system can invoke the request/response services offered by other systems. The *solicit-response* (requestor) and *request-response* (responder) service types are used to implement this paradigm in Edgware.

A solicit-response service can send a request to multiple compatible services using one message.

[Sending a request](#Send_request)

[Handling a request](#Handle_request)

[Response message](#Response)

### <a id="Send_request"></a>Sending a request

A request message is a JSON message of the following form, sent to the system's local Edgware node:

| Field              | Value                              | Description |
| ------------------ | ---------------------------------- | ----------- |
| `op`               | `request`                          |  Identifies a request message. |
| `request-response` | \<target-request-response-service> | An array of IDs (at least one) of the request‐response services to which the request message is to be sent. These are the fully qualified, globally unique names of the services, of the form: \<platform-id>/\<system-id>/\<request-response-serviceid>. |
| `msg`              | \<message-data>                    | The request message payload. This can be a simple string or a JSON object, array, or value. |
| `solicit-response` | \<source-solicit-response-service> | The ID of the local solicit-response service to which the response message(s) are to be be delivered. This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<system-id>/\<solicit-response-service-id>. |
| `correl`           | \<correlation-id>                  | Client-defined correlation ID. Always required. |

The `request` message may also include the following optional field:
 
| Field      | Value               | Description |
| ---------- | ------------------- | ----------- |
| `encoding` | \<message-encoding> | The encoding of the message. The default is ASCII and other encodings are the responsibility of the requester (although the encoding chosen must be supported by the responder). For example, the requester might choose to use a Base64 encoding for the `msg` field; in that case the `encoding` field might be `base64`. |

#### Example   

	{
		"op" : "request",
		"request-response": [
			"<platform-id>/<system-id>/<request-response-service-id>"
		]		    
		"msg" : "<message-data>",
		"solicit-response" : "<platform-id>/<system-id>/<solicit-response-service-id>",
		"correl" : "<correlation-id>"
    }

### <a id="Handle_request"></a>Handling a request

The request message will be delivered to each of the named request-response services, wherever they are on the bus, which then return their responses in a message of the form:

| Field              | Value                              | Description
| ------------------ | ---------------------------------- | ------------- 
| `op`               | `response`                         | Identifies a response message. |
| `solicit-response` | \<target-solicit-response-service> | The ID of the solicit-response service to which the response message is to be delivered (the original requester). This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<system-id>/\<solicit-response-service-id>, and is taken from the original request message.
| `msg`              | \<message-data>                    | The request message payload. This can be a simple string or a JSON object, array, or value. |
| `request-response` | \<source-request-response-service> | The ID of the request-response service that is producing this response message. This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<system-id>/\<request-response-service-id>. |
| `correl`           | \<correlation-id>                  |  The correlation ID from the original request message. Always required. |

The `response` message may also include the following optional field:
 
| Field      | Value               | Description |
| ---------- | ------------------- | ----------- |
| `encoding` | \<message-encoding> | The encoding of the message. The default is ASCII and other encodings are the responsibility of the responder. For example, the responder might choose to use a Base64 encoding for the `msg` field; in that case the `encoding` field might be `base64`. |

#### Example   

	{
		"op" : "response,
		"solicit-response" : "<platform-id>/<system-id>/<solicit-response-service-id>",
		"msg" : "<message-data>",
		"request-response" : "<platform-id>/<system-id>/<request-response-service-id>",
		"correl" : "<correlation-id>"
	}
    
### <a id="Response"></a>Response message

The response message will flow back along the bus and be delivered to the original requester. It will be a JSON message of the form:

| Field              | Value                              | Description |
| ------------------ | ---------------------------------- | ----------- | 
| `op`               | `response`                         | Identifies a response message sent in reply to a corresponding request. |
| `solicit-response` | \<target-solicit-response-service> | The ID of the solicit-response service to which the response message is being delivered. This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<system-id>/\<solicit-response-service-id>, and is taken from the original request message. |
| `msg`              | \<message-data>                    | The request message payload. This can be a simple string or a JSON object, array, or value. |
| `request-response` | \<target-request-response-service> | ID of the request-response service that produced the response message. This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<systemid>/\<request-response-service-id>. |
| `correl`           | \<correlation-id>                  | The correlation ID from the original request message. Always required. |

The `response` message may also include the following optional field:
 
| Field      | Value               | Description |
| ---------- | ------------------- | ----------- |
| `encoding` | \<message-encoding> | The encoding of the message. The default is ASCII and other encodings are the responsibility of the responder. For example, the responder might choose to use a Base64 encoding for the `msg` field; in that case the `encoding` field might be `base64`. |

#### Example   

	{
		"op" : "response",
		"solicit-response" : "<platform-id>/<system-id>/<solicit-response-service-id>",
		"msg" : "<message-data>",
		"request-response" : "<platform-id>/<system-id>/<request-response-service-id>",
		"correl" : "<correlation-id>"
	}
