# Kache

## Goals and Overview

Kache is a decentralised application framework to provide a user- and developer-friendly experience.

It aims to provide these basic concepts:

- Distributed file system with eventual consistency
- EventPub (just like ActivityPub but for machine-friendly events)
- Consistency algorithm
- Automagical best-effort transfering relays and NAT travsal

## Table of Contents

- Goals and Overview
- Kache Network
  - Basic Concepts
  - Working over I2P
- Vaults
  - File System
  - EventPub
- Kache Court
  - Working Process
  - Issues
- Relays
- Word Definitions
- Further Readings
- Authors
- License

## Kache Network

Kache is about connecting different processes across devices. A kache network includes all inter-connecting processes using kache.

````
+---------------------+
|                     |
+-------+ Application +
| Kache |             |
+-------+-------------+
|       I2P           |
+---------------------+
````

Kache and third-party applications both works on I2P, which provides access from any network with consistent addresses even in a mobile environment. Application using kache by OS-agent or the library to access kache's functions. I2P is integrated into the library for complete control.

### Basic Concepts

Kache networks have one home server and at least one device.

![Image: one home server, device zero and device one are connected](./basic_concepts.svg)

A home server is required for network join but is unrequired for the daily functions of kache. A Home server is a "device" but in a special role, served as a backup and a gatekeeper in kache.

Except stated otherwise, any kache functionality must be available whether the home server is online or offline. 

![Image: home server is offline. Device zero and device one are connected each other](./basic_concepts_without_homesvr.svg)

Such architecture works like "fediverse" but not exactly is, could be called "weak-fediverse", which is able to continue its functionality during the server on network is down until every device is done.

![Image: Server A, B, C inter-connected. Clients are connected to servers.](./fedi_arch.svg)

### Working over I2P

Kache network is being built over the I2P network.

A Home server may be connected through a public network rather than the I2P network for limited functions. These functions are network join, signing in, information exchanging between two home servers or other implicitly stated.
