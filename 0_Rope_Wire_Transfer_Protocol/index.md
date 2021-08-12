# Rope Wire Transfer Protocol

Rope Wire Tansfer Protocol is a role-less abstract secure tunnel protocol. It's intended to provide secure and verifiable data transfering in most environment.

## Goals

Rope Wire Transfer Protocol should be:

- easy to implement
- avaliable to most environment and purpose
- providing secure data transfering

## Table of Contents

- Goals
- Overview
- Messages and Frames
  - Expression
  - Packing and Unpacking
- Protocol Message
  - Layout
  - Control Codes
    - DATA
    - SETOPT
    - ASKOPT
    - User-defined Codes
  - Options
    - PUBKEY
    - SECKEY
    - TIME
    - User-defined Options
- Seal Mode
- Public-key Mode
- Secret-key Mode
- Further Readings
- Reference Implementation
- License

## Overview

Rope Wire Transfer Protocol is an abstract protocol, that means: the runtime details are based on how it being implemented. RWTP depends on two concepts: messages and frames. Any protocol message will be packed as a frame which ready to transfered over transports. The packing layout comes from "MessagePack".

RWTP have three different modes for situations: seal, public-key and secret-key. The required encryption methods are all included in "sodium" library. Seal mode is the most special mode in the three, the security depends on a pre-shared key pair called "network key". The latter two will create a short-term "transport key" for a session.

## Messages and Frames

Frame is atomic unit of data. One frame can have zero or more byte(s) data.

Message is one or more frame(s).

These concepts are defined in abstract, should be defined by implementation to be used in reality.

### Expression

````
f1 | f2 | f3 | ...
````
The messages can be described by above syntax. `|` works as separators to frames, `...` means there can be infinite number of frames.

````
f1(uint8_t) | f2(uint32_t) | f3(string) | ...
````
Most frame in message have specific length, this document use parentnesses to note the specific type, most from C's fixed length int types. A exception is `string`, which is a series of uint8_t with `0` as end, mostly called C-string.  These are types used in this document:

- `uint8_t` 8 bits
- `string` variable-length 8 bits, with `0` as end
- `bX` X bytes binary

### Packing and Unpacking

RWTP uses "MessagePack" to pack and unpack messages. Every frame will be serialised as a "bin" block.


## Protocol Message

Any protocol message have a control code in the front:

````
CTL(uint8_t) | ...
````

The control code helps remote identify what this message used for.

### Control codes

Control code is a unsigned 8-bit integer.

- DATA `0`
- SETOPT `1`
- ASKOPT `2`
- User-defined from `64` to `89`

#### DATA

This type of message is used for transfering user's messages.

````
0 | user_message...
````

#### SETOPT

This type of message is used for set option for the session.

````
1 | OPT(uint8_t) | option_values...
````

Avaliable options are described in "Options" section.

#### ASKOPT

This type of message is used for ask option from remote.

````
2 | OPT(uint8_t)
````

Avaliable options are described in "Options" section.

#### User-defined Codes

````
UCTL(uint8_t) | user_message...
````

### Options

Options' key is unsigned 8-bit integer. The options described here are used by SETOPT and ASKOPT messages.

#### PUBKEY
Set public key and IV.

Option values:

````
PUBKEY(b32) | IV(b48)
````

#### SECKEY
Set secret key and secret stream header.

Option values:
````
SECKEY(b32) | IV(b24)
````

#### TIME
Set time.

Option values:
````
TIME(string)
````

The `TIME` must be a string that can be parsed to a 64-bit integer.

#### User-defined Options
The range for user-defined options is from `64` to `89`.

Option values:
````
user_message...
````

The `user_message` should be returned to user.

### Sending or Receiving Message

## Seal Mode

## Public-key Mode

## Secret-key Mode

## Further Readings

- MessagePack specification https://github.com/msgpack/msgpack/blob/master/spec.md
- Sodium document https://doc.libsodium.org/

## Reference Implementation

- librope https://github.com/kacheproject/librope

## License

Public Domain
