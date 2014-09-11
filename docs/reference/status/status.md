---
layout: default
title: Status messages and codes
---

[Interface status messages](#ISM)

[Status and error codes](#SEC)

[Operation codes](#OpCodes)

[Entity codes](#EntityCodes)

### <a id="ISM"></a>Interface status messages

When Edgware sends a status in response to an operation it is a JSON message of the following form:

| Field    | Value             | Description |
| -------- | ----------------- | ----------- | 
| `op`     | `status`          | Identifies a status message. |
| `correl` | \<correlation-id> | Client-defined correlation ID, specified in the inital request message (if any). |
| `status` | \<status-code>    | The returned status code. |
| `msg`    | \<status-message> | The returned status message (i.e. a detail message containing more information). |

The `status` message may also include the following optional field:
 
| Field      | Value               | Description |
| ---------- | ------------------- | ----------- |
| `encoding` | \<message-encoding> | The encoding of the message. The default is ASCII and other encodings are the responsibility of the publisher. For example, the publisher might choose to use a Base64 encoding for the `msg` field; in that case the `encoding` field might be `base64`.

Asynchronous interfaces such as MQTT, unless otherwise specified, will generally not generate a status message unless a correlaton ID is included in the request.

However, messages containing syntax errors (i.e. messages that are not parsable by Edgware), or that result internal run-time errors in Edgware, will generate unsolicited response messages without a correlation ID.

Synchronous interfaces such as HTTP always generate status messages.

####Example   

	{
		"op" : "status",
		"correl" : "<correlation-id>",
		"status" : "<status-code>",
		"msg" : "<status-message>",
		"encoding" : "<message-encoding>"
	}

An "OK" status will be of the form:

	{
		"op" : "status",
		"correl" : "<correlation-id>",
		"status" : "00000",
		"msg" : "OK",
		"encoding" : "ascii"
	}

## <a id="SEC"></a>Status and error codes

A status code is composed of three fields:

- A one digit hexadecimal error code: indicates if the error occurred during parsing of the message, or actioning of the message.
- A two digit hexadecimal operation code: the operation being performed.
- A two digit hexadecimal entity code: the entity to which the operation was being applied. A status code of `"00000"` indicates success.

### Error codes

| Code | Meaning |
| ---- | ------- |
| 1    | Parse error: an error parasing the JSON |
| 2    | Parse error: an error parasing the JSON |

### <a id="OpCodes"></a>Operation codes

| Code | Meaning |
| ---- | ------- |
| 01   | Error with no operation |
| 02   | Registration error |
| 03   | Deregistration error |
| 04   | Query error |
| 05   | State change error |
| 06   | Publish error |
| 07   | Subscribe error |
| 08   | Unsubscribe error |
| 09   | Notification error |
| 0A   | Request error |
| 0B   | Response error |

### <a id="EntityCodes"></a>Entity codes

| Code | Meaning |
| ---- | ------- |
| 01 | Error with no entity |
| 02 | JSON error |
| 03 | Node entity error |
| 04 | Local node entity error |
| 05 | Node type entity error |
| 06 | Bearer entity error |
| 07 | Bearer type entity error |
| 08 | Platform entity error |
| 09 | Platform type entity error |
| 0A | System entity error |
| 0B | System type entity error |
| 0C | Service type entity error |
| 0D | User entity error |
| 0B | User type entity error |
