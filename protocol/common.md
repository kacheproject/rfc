# Protocol Common

Kache perfer uses ZeroMQ as its network basement. ZeroMQ have bundled with many useful features about network programming to prevent many problems about directly dealing with genernal network stack ([Why ZeroMQ](./why_zeromq.md)).

Instead of packet or stream, the basic concepts in tranferring of zeromq is frame. Frame is a atomic element of data. One message can contain one or more frames. The message with two or more frames called multipart message.

ZeroMQ define some patterns of "socket". If you want to known more about ZeroMQ please navigate to [ZeroMQ Guide](zguide.zeromq.org), which is a free complete book about ZeroMQ. This book does not covered many ZeroMQ improvments which are added after the book released, these new features will be described when required. 

## How Messages Constructed
All of messages transfered by ZeroMQ used in kache will have same structure (unless specially described): command, headers and playload.
````
| command | headers (zero or more) | <empty> | data (zero or more) |
````
- command frame always leads one message
- zero or more header frames follow command frame
- a empty frame used to identify the start of data frames
- the number of data frames can be zero or more
