# RFC0: Rope

Rope is a decentralised transport protocol. It acts like OSI layer 4 but works in the application layer.

Rope provides "EventPub", the broadcast part, and "Tunnel", the peer to peer part. Both are using "Network Database", which stores peer information.

## Table of Contents

- Overview
  - Network Database
  - Reachability
- EventPub
  - Internal Events
- Tunnels
  - Services & Entries

## Overview

Rope has two parts: EventPub and Tunnels. EventPub is used to broadcast messages to the whole network. Tunnels can transfer data peer to peer. Besides user-defined events, Rope uses EventPub to spread internal knowledge of the network. The internal knowledge is collected and used to maintain the network database.

**Peers** are two devices can equally transfer data in two way.

**Physical addresses** are the transport used to transfer data. Rope has "entry", which can be used to identify multiple physical addresses, may be considered as one kind of "virtual address".

**Services** are pairs of service names and 128-bit entries. The first 64 bits of an entry are the router identity, and the latter 64 bits is a random number.

**Routers** are the software used by peers to join the network.

### Network Database

Network database should store information about "Peer", "Physical address" and "Services".

### Reachability

## EventPub

### Internal Events

## Tunnels

## License

Public Domain
