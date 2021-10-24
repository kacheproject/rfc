# RFC0: Rope

Rope is a decentralised transport protocol. It acts like OSI layer 4 but works in the application layer.

Rope provides "EventPub", the broadcast part, and "Tunnel", the peer to peer part. Both are using "Network Database", which stores peer information.

## Table of Contents

- Overview
  - Network Database
  - Reachability
- EventPub
  - Data Layout
  - Internal Events
- Tunnels
  - Services & Entries

## Overview

Rope has two parts: EventPub and Tunnels. EventPub is used to broadcast messages to the whole network. Tunnels can transfer data peer to peer. Besides user-defined events, Rope uses EventPub to spread internal knowledge of the network. The internal knowledge is collected and used to maintain the network database.

**Peers** are devices are designed can equally transfer data in two ways.

**Physical addresses** are the transport's addresses used to transfer data. Rope has "entry", which can be used to identify multiple physical addresses, may be considered as one kind of "virtual address".

**Services** are pairs of service names and 128-bit entries. The first 64 bits of an entry are the router identity, and the latter 64 bits is a random number.

**Routers** are the software used by peers using this procotol to join the network.

### Network Database

Network database should store information about "Peer", "Physical address" and "Services". The information help Tunnels and EventPub maintain connections and might allow access from applications.

### Reachability

## EventPub

### Data Layout

Formal definition:

````
event = event_name flags router_id router_clk user_msg
event_name = variant length binary
flags = 1OTECT
router_id = 8OTECT
router_clk = 8OTECT
user_msg = variant length binary
````

`event_name` is a string of the event's name.

`flags` is an unsigned 8-bit number. The first bit is the forwarded mark. If the forwarded mark is 1, the sender is not the original sender of this message. The rest bits are reserved for the future.

`router_id` is an unsigned 8-bit number (Big endian).

`router_clk` is an unsigned 8-bit number (Big endian). It's the time of the logical clock from the router.

`user_msg` is variant length binary.


### Internal Events

#### Ticktock

## Tunnels

## License

Public Domain
