# Rope Protocol, version 6 (RPv6)

RPv6 is a layer 3 and 4 protocol covered the usage of IP and UDP. Designed to be transfered over any other protocol, for example WireGuard or even UDP over IP, try to be compact as it can and be compatiable to some WireGuard library which verify the IP packets.

- Compat data layout (header only takes 40 octets - as the smallest IPv6 header) with minor IPv6 compability.
- Datagram-oriented transport.

## Working Draft

This document is in progress. We are still discussing and changes may be made in future.

## Data Layout

### Frame
````
+ ------------------ + -------------------------- +
| Header (40 octets) | Payload (0 - 65535 octets) |
+ ------------------ + -------------------------- +
````
Frame is atomic unit of data. The most payload size is 65535 bytes as the upper limit of unsigned 16-bit integer. All integers in a frame is transfered in Big-endian form.


### Header
````
0                                                                                                                   31
+ ---------------- + ------------------ + --------------- + ------------------------------------------------------- +
| VERSION (4 bits) | RESERVED0 (4 bits) | flags (1 octet) |                  src_port (2 octets)                    |
+ ---------------- + ------------------ + --------------- + ------------------------------------------------------- +
|             payload_length (2 octets)                   |                  dst_port (2 octets)                    |
+ ------------------------------------------------------- + ------------------------------------------------------- +
|                                                                                                                   |
|                                                src_addr (16 octets)                                               |
|                                                                                                                   |
|                                                                                                                   |
+ ------------------------------------------------------------------------------------------------------------------+
|                                                                                                                   |
|                                                dst_addr (16 octets)                                               |
|                                                                                                                   |
|                                                                                                                   |
+ ------------------------------------------------------------------------------------------------------------------+
````
VERSION is always `6`.

## Flags
Currently, no flag is defined. It should be fill with zero and the behaviours of the other values are undefined.

## License
CC0
