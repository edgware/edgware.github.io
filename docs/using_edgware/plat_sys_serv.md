---
layout: default
title: Platforms, systems and services
---
Edgware *services* are the core building blocks for apps. A collection of related services is referred to as a *system*. One or more systems connect to a *platform*, which in turn connects to an Edgware *node*.

The platform is a logical entity that provides a unique address for a group of systems on the bus. An app could be a platform, but platforms will often map to a corresponding physical entity such as a vehicle, a building, a person etc. Where such a mapping exists the platform ID will often follow the naming convention applied to the corresponding physical entity. For example, the ID for an Edgware platform representing a vehicle could be the vehicle registration. That said, you get to choose the names for your platforms, systems and services.

We address things attached to the bus using their platform ID rather than the ID of the node to which they are attached. So, to address a specific system, we use a 2-part name of the form ```<platform-id>/<system-id>```. To address a specific service we use a 3-part name of the form ```<platform-id>/<system-id>/<service-id>```.

Addressing systems and services via their platform enables support for dynamic network topologies and mobile systems. Platforms may move between nodes over time (the platforms themselves might be mobile and/or nodes might come and go) however their address on the bus, and that of their systems and services, remains the same to the apps that use them. Edgware is responsible for resolving the logical address to an actual network address.
