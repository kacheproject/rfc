# Rope Peer Discovery Protocol (RPDP)
Goals:

- Compact.
- Safe to update.
- Suitable for embedding devices.
- Works over RPv6 (rfc0).

Peers need to exchange information between peers to know other peers on the network.

## Message Layout
````
+ ----------------- + ---------------- +
|  MSG_TYP (8bits)  |  CONTENT (rest)  |
+ ----------------- + -----------------
````
Since any rope packet includes length, we don't need the length field in messages. But the length of the whole message should be limited to 2048 bytes to ensure embedding devices with small memory equipped can parse messages.

## Message Types
`MSG_TYP` is an unsigned 8-bit integer, which is the indicator of content. It's the approach used in ICMP. Peers must ignore messages with unknown `MSG_TYP`.
We use Messagepack format, a JSON-like, in `CONTENT`. Messagepack is compact enough for embed devices, and we keep using its map type in `CONTENT` to keep flexibility.

- ND_SYNC (`0`, broadcast)
- ND_BYE (`1`, broadcast)
- ND_ASK (`2`)
- ND_SET (`3`)

````
lifetime = ND_SYNC *msg
msg = ND_SYNC | ND_ASK | ND_SET | ND_BYE
````

## ND_SYNC
Tell the other machines the peer IDs you know they don't know (the delta).

Fields:
- `known` (array of u128, upper limit 64 entries)

Sending when:
- Populating the local database (at startup).
- Reply to the others' ND_SYNC.

In the first case, it may only contain the ID of the sending peer.

Recommend to delay random seconds before calculating delta for reducing network load.

## ND_BYE
Part of a graceful shutdown. All received peers should know this peer as shutdown.

This message comes with no field. Use the RPv6 header to figure out the sending peer.

Sending when:
- Graceful shutdown

## ND_ASK
Ask details for a peer. One or all peers on the network may receive this message.

Fields:
- `id` (u128)
- `q` (list of integer)

`q` is a list of questions for answers:
- `1`: Public key
- `2`: Physical wires

Only the specific peer of `id` should reply to the message when broadcasting.

## ND_SET
Reply to an ND_ASK. Peers may send multiple times to reply to one ND_ASK.

Fields:
- `id` (u128)
- `answers` (map. Integer is key, the answer is value. See ND_ASK for the question list.)

Answers type:
- `1`: base64 string of public key
- `2`: URI string of external address

## Service Discovery Extension
Any RPDP peer may implement the Service Discovery Extension. This extension provides availability to track services on the network.

### Service
A service includes:

- Host peer id
- Port
- Application
- Arguments

It can be encoded as an URI: `kache://58a69f7543:4521?user=dGFua21hbkBrYWNoZS5leGFtcGxlLm9yZw`, in follow of `<Application>://<Host Peer ID>:<Port>[?<Arguments1>=<Value1>[&<Argument2>=<Value2> [&...]]]`.

### Messages

- SDExt_QUERY (`10`, broadcast)
- SDExt_SYNC (`11`)

````
lifetime = SDExt_SYNC *msg
msg = SDExt_QUERY | SDExt_SYNC 
````

### SDExt_QUERY

### SDExt_SYNC
