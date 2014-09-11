---
layout: default
title: Notifications
---

A running system can send individual ad hoc messages (i.e. notfications) for consumption by other systems. Notification messages differ from data feed messages in that they are sent to a set of recipients (who have indicated that they are able to receive them) that is determined by the sender; conversely recipients of *data feed* messages must have explicitly requested (subscribed to) them.

Note that the target system/service that receives the message must also be running.

[Send a notification](#Send_notification)

[Notification message](#Notification)

### <a id="Send_notification"></a>Send a notification

A notification message is a JSON message of the following form, sent to the system's local Edgware node:

| Field          | Value                          | Description |
| -------------- | ------------------------------ | ----------- | 
| `op`           | `notify`                       | Identifies a notification message. |
| `listener`     | \<target-listener-service>     | An array of IDs (at least one) of the listener services to which the notification message is to be sent.  These are the fully qualified, globally unique names of the services, of the form: \<platform-id>/\<system-id>/\<listener-service-id>. |
| `msg`          | \<message-data>                | The notification message payload. This can be a simple string or a JSON object, array, or value. |
| `notification` | \<source-notification-service> | The ID of the notification service that produced this notification. This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<system-id>/\<notification-service-id>. |

The `notify` message may also include the following optional fields:
 
| Field      | Value               | Description |
| ---------- | ------------------- | ----------- |
| `encoding` | \<message-encoding> | The encoding of the message. The default is ASCII and other encodings are the responsibility of the notifier. For example, the notifier might choose to use a Base64 encoding for the `msg` field; in that case the `encoding` field might be `base64`. |
| `correl`   | \<correlation-id>   | Client-defined correlation ID, present if a status response is required.

This message will be delivered to each of the named listener services, wherever they are on the bus.

####Example   

	{
		"op" : "notify",
		"listener" : [
			"<platform-id>/<system-id>/<listener-service-id>"
		],
		"msg" : "<message-data>",
		"notification" : "<platform-id>/<system-id>/<notification-service-id>",
		"correl" : "<correlation-id>"    
	}

### <a id="Notification"></a>Notification message

Received notifications are JSON messages of the form:

| Field          | Value                          | Description |
| -------------- | ------------------------------ | ----------- | 
| `op`           | `notification`                 | Identifies a received notification message. |
| `listener`     | \<target-listener-service>     | The ID of the listener service to which the notification message is being sent (the recipient). This is the fully qualified, globally unique name of the services, of the form: \<platform-id>/\<system-id>/\<listener-service-id>. |
| `msg`          | \<message-data>                | The notification message payload. This can be a simple string or a JSON object, array, or value. |
| `notification` | \<source-notification-service> | The ID of the notification service that produced the message (the sender). This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<system-id>/\<notification-service-id>. |

The `notification` message may also include the following optional field:

| Field      | Value               | Description |
| ---------- | ------------------- | ----------- |
| `encoding` | \<message-encoding> | The encoding of the message. The default is ASCII. |

####Example   

	{
		"op" : "notification",
		"listener" : "<platform-id>/<system-id>/<listener-service-id>",
		"msg" : "<message-data>",
		"notification" : "<platform-id>/<system-id>/<notification-service-id>"
	}


