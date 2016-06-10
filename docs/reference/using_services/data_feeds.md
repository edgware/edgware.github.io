---
layout: default
title: Data feeds
---

Once registered and running, the systems amd services of Edgware are available for use. One of the most common functions on the bus is publish/subscribe, known in Edgware as data feeds.  

A system can publish one or more data feeds (e.g. sensor telemetry) for consumption by other systems. The system must be registered, and one or more output-feed services defined to identify the data being shared.

[Publish a message to an output-feed](#Publish)

[Subscribe to an output-feed](#Subscribe)

[A feed message](#Feed_message)

[Unsubscribe from an output-feed](#Unsubscribe)

### <a id="Publish"></a>Publish a message to an output feed

To publish data, a system simply sends a JSON message of the following form to its local Edgware node; Edgware will then take care of delivering the message to all current subscribers:
 
| Field         | Value                 | Description |
| ------------- | --------------------- | ----------- |
| `op`          | `publish`             | Identifies a publish message. |
| `output-feed` | \<target-output-feed> | The ID of the output-feed to which the payload is to be publishd. This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<system-id>/\<output-feed-service-id>. |
| `msg`         | \<message-data>       | The message payload to be published. This can be a simple string or a JSON object, array, or value.

The `publish` message may also include the following optional fields:
 
| Field      | Value               | Description |
| ---------- | ------------------- | ----------- |
| `encoding` | \<message-encoding> | The encoding of the message. The default is ASCII and other encodings are the responsibility of the publisher. For example, the publisher might choose to use a Base64 encoding for the `msg` field; in that case the `encoding` field might be `base64`.
| `correl`   | \<correlation-id>   | Client-defined correlation ID, present if a status response is required.

#### Example   

    {
		"op" : "publish",
		"output-feed" : "<platform-id>/<system-id>/<service-id>",
		"msg" : "<message-data>",
		"correl" : "<correlation-id>"
    }

### <a id="Subscribe"></a>Subscribe to an output feed

Correspondingly, a system can request the delivery of (i.e. subscribe to) messages from output-feed services attached to its local and/or *remote* Edgware nodes (in fact the subscriber is unaware of the physical source of the data feed -- Edgware will work that out). A subscription request is a JSON message of the following form:

| Field          | Value                 | Description |
| -------------- | --------------------- | ----------- | 
| `op`           | `subscribe`           | Identifies a subscription message. |
| `output-feeds` | \<source-output-feed> | An array of IDs (at least one) of the output-feed services producing the information to which subscriptions are being made. These are the fully qualified, globally unique names of the services, of the form \<platform-id>/\<system-id>/\<output-feed-service-id>. |
| `input-feed`   | \<target-input-feed>  | The ID of the local input-feed service to which messages will be delivered. This is the fully qualified, globally unique name of the service, of the form \<platform-id>/\<system-id>/\<output-feed-service-id>. |
| `correl`       | \<correlation-id>     | Client-defined correlation ID to identify the response. |

Edgware supports wildcard subscriptions, where the "*" wildcard character can be used in plaform IDs, system IDs and service IDs. In addition the Edgware Registry can be queried to locate services of a specific name or type.

A subscription message always generates a response of the form:

| Field          | Value                 | Description |
| -------------- | --------------------- | ----------- | 
| `op`           | `subscriptions`       | Identifies a subscription response message. |
| `output-feeds` | \<source-output-feed> | An array of IDs (at least one) of the output-feed services to which subscriptions have been made.  These are the fully qualified, globally uniques name of the services, of the form: \<platform-id>/\<system-id>/\<output-feed-service-id>. |
| `correl`       | \<correlation-id>     | Client‐defined correlaton ID to identify the corresponding subsription request.|

#### Example   

	{
		"op" : "subscribe",
		"output-feeds" : [
			"<platform-id>/<system-id>/<output-feed-service-id>"
		]
		"input-feed" : "<platform-id>/<system-id>/<input-feed-service-id>",
		"correl" : "<correlation-id>"
	}
 
Using a wildcard:
   
	{
		"op" : "subscribe",
		"output-feeds" : [
			"*/<system-id>/<output-feed-service-id>",
		]
		"input-feed" : "<platform-id>/<system-id>/<input-feed-service-id>",
		"correl" : "<correlation-id>"
    }

Subscription messages will generate a response of the form:
   
	{
		"op" : "subscriptions",
		"output-feeds" : [
			"<platform-id>/<system-id>/<input-feed-service-id>",
			"<platform-id>/<system-id>/<input-feed-service-id>",
			"<platform-id>/<system-id>/<input-feed-service-id>"
		]
		"correl" : "<correlation-id>"
	}

### <a id="Feed_message"></a>Feed message

JOSN messages delivered in response to a subscription will be of the form:

| Field         | Value                 | Description |
| ------------- | --------------------- | ----------- | 
| `op`          | `feed-message`        | Identifies a feed message delivered in respose to an active subscription. |
| `output-feed` | \<source-output-feed> | The ID of the output-feed service that produced the message (the sender). This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<system-id>/\<output-feed-service-id>. |
| `msg`         | \<message-data>       | The data feed message payload. This can be a simple string or a JSON object, array, or value. |
| `input-feed`  | \<input-feed-service> | The ID of the input-feed service to which the feed message is being delivered (the recipient). This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<system-id>/\<input-feed-service-id>. |

If the encoding of the message payload (`msg`) is not ASCII then the following optional field will be included:

| Field      | Value               | Description |
| ---------- | ------------------- | ----------- |
| `encoding` | \<message-encoding> | The encoding of the message. The default is ASCII. |

#### Example   

	{
		"op" : "feed-message",
		"output-feed" : "<platform-id>/<system-id>/<output-feed-service-id>",
		"msg" : "<message-data>",
		"input-feed" : "FOB123/bft/vehicle-pos"
	}
    
### <a id="Unsubscribe"></a>Unsubcribe from an output feed

An unsubscribe request for one or more output-service data feeds is a JSON message of the following form:

| Field        | Value                | Description |
| ------------ | -------------------- | ----------- | 
| `op`         | `unsubscribe`        | Identifies an unsubscribe message. |
| `input-feed` | \<target-input-feed> | The ID of the local input-feed service to which messages are being delivered. This is the fully qualified, globally unique name of the service, of the form: \<platform-id>/\<system-id>/\<input-feed-service-id>. |

The `unsubscribe` message may also include the following optional field:

| Field          | Value                 | Description |
| -------------- | --------------------- | ----------- | 
| `output-feeds` | \<source-output-feed> | An array of IDs (at least one) of output-feed services with active subscriptions linked to the target input-feed. The subsriptions to these feeds will be cancelled. If the list of the output feeds is omitted then all the subscriptions for the target input feed will be cancelled. The feed IDs are the fully qualified, globally unique names of the services, of the form: \<platform-id>/<system-id>/<output-feed-service-id>. |
| `correl`       | \<correlation-id>    | Client-defined correlation ID, present if a status response is required. |

The message can include wildcards in the `output-feeds` service identifier list that will be matched against the active subscriptions linked to the specified target input feed.

Note that an "unsubscribe" is required for every corresponding "subscribe".

#### Example   

The following message will unsubscribe from all feeds associated with the named input-feed:

	{
		"op" : "unsubscribe",
		"input-feed" : "<platform-id>/<system-id>/<input-feed-service-id>",
		"correl" : "<correlation-id>"
	}

The following message will unsubscribe from the specified feeds associated with the named input-feed:

	{
		"op" : "unsubscribe",
		"input-feed" : "<platform-id>/<system-id>/<input-feed-service-id>",
		"output-feed" : [
			"<platform-id>/<system-id>/<output-feed-service-id>"
		],
		"correl" : "<correlation-id>"
	}
