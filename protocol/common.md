# Protocol Common

Kache perfer uses ZeroMQ as its network basement. ZeroMQ have bundled with many useful features about network programming to prevent many problems about directly dealing with genernal network stack ([Why ZeroMQ](./why_zeromq.md)).

Instead of packet or stream, the basic concepts in tranferring of zeromq is frame. Frame is a atomic element of data. One message can contain one or more frames. The message with two or more frames called multipart message.

ZeroMQ define some patterns of "socket". If you want to known more about ZeroMQ please navigate to [ZeroMQ Guide](https://zguide.zeromq.org), which is a free complete book about ZeroMQ. This book does not covered many ZeroMQ improvments which are added after the book released, these new features will be described when required. 

## How Messages Constructed
All of messages transfered by ZeroMQ used in kache will have same structure (unless specially described): command, headers and playload.
````
| command | headers (zero or more) | <empty> | data (zero or more) |
````
- command frame always leads one message
- zero or more header frames follow command frame
- a empty frame used to identify the start of data frames
- the number of data frames can be zero or more

## Message Describing Protocol in this RFC
We use a unprotocol-like syntax to describe messages used in kache.

````
hello = $, api_version, name, software, supported_feature_sets
REPLY hello = "hello", api_version, name, software, supported_feature_sets
REPLY hello = "bye", api_version, name, software, supported_feature_sets
````

- `$` means a string same as the symbol (in this case, "hello")
- In the comma-separated list, the first element is command frame and the rest are data frames.
- Headers are not presented in this represent.
- the prefix `REPLY` means it should be one of the possible replies of the request


Sometimes we need to explain values, there is how:
````
api_version = string of the APIs supported by software # this is a comment
get_api_version = $
REPLY get_api_version = "OK", api_version
````
The life of the explain is based on the context.

You also can refer a symbol to a present.
````
OK = "OK"
STATUS = 204 | 200 # That means we choose one from 204 and 200
REPLY check_status = OK, STATUS
````


The syntax is tend to be readable and you can try many ways to be comfortable while writing.
