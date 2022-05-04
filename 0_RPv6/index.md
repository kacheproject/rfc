# Rope Protocol, version 6 (RPv6)

RPv6 is a protocol that works on OSI layers 3 and 4, an alternative to IP and UDP. 

- Compact data layout (header only takes 40 octets - as the smallest IPv6 header) with minor IPv6 compatibility.
- Best-effort datagram transport.
- Mobile-friendly.

## Working Draft

This document is in progress. We are still discussing, and changes may be made in future.

## Data Layout

### Frame
````
+ ------------------ + -------------------------- +
| Header (40 octets) | Payload (0 - 65535 octets) |
+ ------------------ + -------------------------- +
````
A frame is the atomic unit of data. The most payload size is 65535 bytes as the upper limit of an unsigned 16-bit integer. All integers in a frame are encoded in Big-endian form.

In the actual case, a payload's max length may vary depending on the transport.


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

- VERSION is always `6`.

## Flags
No flag defined -- reserved for the future.

## Ports

- `src_port` defines the source port.
- `dst_port` defines the destination port.

Ports can help to identify the data stream.

| Range         | Name        | Description                                          |
|---------------|-------------|------------------------------------------------------|
| [0, 255]      | Internal    | Reserved for rope related services. |
| [256, 1023]   | Platform    | Reserved for platform's specific services.                                                     |
| [1024, 65535] | Application | Applications.                                                     |



## Addresses

- `src_addr` defines the source address.
- `dst_addr` defines the destination address.

As of IPv6, an RPv6 address takes 16 bytes of space. Addresses in RPv6 don't have other means than unique identities.

The application can use these ids for other usages.

## License
<p xmlns:dct="http://purl.org/dc/terms/" xmlns:vcard="http://www.w3.org/2001/vcard-rdf/3.0#">
  <a rel="license"
     href="http://creativecommons.org/publicdomain/zero/1.0/">
    <img src="http://i.creativecommons.org/p/zero/1.0/88x31.png" style="border-style: none;" alt="CC0" />
  </a>
  <br />
  To the extent possible under law,
  <a rel="dct:publisher"
     href="https://github.com/kacheproject">
    <span property="dct:title">The Authors of Kache RFCs</span></a>
  has waived all copyright and related or neighboring rights to
  <span property="dct:title">RFC0: Rope Protocol, version 6</span>.
</p>
