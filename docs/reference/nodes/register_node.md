---
layout: default
title: Register a node
---

To register a node as a neighbour of the local Edgware node, a JSON message of the following form is sent to the local Edgware node:

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
        <td><code>register:node</code></td>
        <td>Identifies a node registration message.</td>
    </tr>
    <tr>
        <td><code>id</code></td>
        <td></td>
        <td>&lt;node-id&gt;</td>
        <td>The ID of the node to be registered.</td>
    </tr>
    <tr>
        <td colspan="4">Each node must define one or more network interfaces using the following fields:</td>
    </tr>
    <tr>
        <td><code>interfaces</code></td>
        <td></td>
        <td></td>
        <td>Identifies the list of interfaces for this node.</td>
    </tr>
    <tr>
        <td rowspan="2"></td>
        <td><code>node-interface</code></td>
        <td>&lt;node-interface&gt;</td>
        <td>The name of the network interface used by the node (e.g. "en0").</td>
    </tr>
    <tr>
        <td><code>address</code></td>
        <td>&lt;node-address&gt;</td>
        <td>The network address of the node in the form of a URI, for example "ip:// 10.10.1.2:1885".</td>
    </tr>
    <tr>
        <td colspan="4">The <code>register:node</code> message may also include the following optional fields:</td>
    </tr>
    <tr>
        <td><code>desc</code></td>
        <td></td>
        <td>&lt;node-description&gt;</td>
        <td>A free text description of the node.</td>
    </tr>
    <tr>
        <td><code>attr</code></td>
        <td></td>
        <td>&lt;unique-node-attributes&gt;</td>
        <td>A JSON object defining a set of attributes associated with the node. Node attributes are not defined by Edgware.</td>
    </tr>
    <tr>
        <td><code>correl</code></td>
        <td></td>
        <td>&lt;correlation­‐id&gt;</td>
        <td>Client-defined correlation ID, present if a status response is required</td>
    </tr>
</table>


#### Example   

	{
		"op" : "register:node",
		"id" : "<node-id>",
		"interfaces" : [
			{
				"node-interface" : "en1",
				"address" : "ip://10.10.1.2:1885"
			}
		]
	}
    
