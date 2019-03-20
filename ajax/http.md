## HTTP

### Test points:
#### [1. What is HTTP?](#http)

#### [2. Standard ports](#ports)

#### [3. Know TCP/UDP](#tcpudp)

#### [4. Contents of a HTTP request](#contents)

#### [5. HTTP methods](#methods)

#### [6. What is URL encoding?](#encoding)

#### [7. Categories of responses](#responses)
---
<a name="http"></a>
### What is HTTP?
HTTP is the Hypertext Transfer Protocol. It is primarily used on the WWW for serving websites and their resources. It can be used with many types of resources, like images, binary files, HTML, and so on.

HTTP is __stateless__, the connection is closed after __Request__ is received and corresponding __Response__ is sent. There is no information kept between requests.
<a name="ports"></a>
### Standard ports

HTTP is encapsulated inside TCP/IP, and is generally on __port 80 for http, for 443 for https__.

<a name="tcpudp"></a>
### TCP vs UDP

___TCP___ or __Transmission Control Protocol__ is used to ensure packets arrive at their destination using a connection.

___UDP___ or __User Datagram Protocol__ is less reliable because it does not ensure that packets arrive.

### TCP
#### Connection Establishment
TCP operates with a three-way handshake that can be written as: `SYN, SYN-ACK, ACK`

![TCP handshake diagram](https://i.imgur.com/L2gpGpO.png)

#### Data Transfer
First, send an HTTP request using sequence number, then get HTTP response also with a sequence number.

![TCP data transfer diagram](https://i.imgur.com/7AN93hZ.png)

#### Closing Connection
Closing the connection is a four way handshake:

![TCP closing connection handshake](https://i.imgur.com/yFMXbSK.png)

<a name="contents"></a>
### What's in an HTTP request?
![HTTP contents chart](https://i.imgur.com/zmStOHW.png)

__The typical HTTP request has:__
- __A request line__: This contains the method, URI (A URI is used to identify a resource but can be something other than a URL), the HTTP version, and a CRLF to signify the next line.
- __Header__: HTTP 1.1 ___REQUIRES___ the __Host:__ header. The `Host` header is used to provide the host and port information from the target URI, which lets the server distinguish among resources from a single client. __User-Agent__ is also pertinent, it's used for client software identification.
- __Body__: which is totally optional and contains the body of the request, this can be different data types but is most commonly HTML.

<a name="methods"></a>
### HTTP Request methods
Method|Description
---|---
GET|Retrieve resource to URI
POST|Store/send data to server
HEAD|Retrieve header (not body) at URI
PUT|Make message body new resource at URI
OPTIONS|What methods are allowed?
DELETE|Remove the resource at URL
TRACE|Echo request back
CONNECT|Proxy Request

`GET` and `POST` are the most used. If you use `POST`, you also need to send a header field indicating the media type. *Speculative*

<a name="encoding"></a>
### URL Encoding
URL encoding is when certain characters are encoded to their hexadecimal values to prevent problems with parsing. Extremely pertinent to things like spaces in URL's.

<a name="responses"></a>
### HTTP response
![HTTP response chart](https://i.imgur.com/sTM1mFm.png)

### Status codes
Status codes are 3 digit integers with status messages. The message can change, but the integer should stay pretty standard. The integer is generally for the computer, whereas the message is usually for humans. The first digit specifies the general type of the message, and the second and third digits give the specific message of that type.

Number|Type
---|---
1xx|Informational messages
2xx|Success messages
3xx|Redirection messages
4xx|Client error messages
5xx|Server error messages

Some of the most common status codes are:

Code|Meaning
---|---
200|OK, this means that the request was successfully carried out.
301|Moved permanently, this means that the resource you're looking for has been permanently moved to a new location.
404|The resource is no longer available.
403|Access to the resource is forbidden. Not an authentication problem, you just can't access the resource.
500|Internal server error, this is the general "The server messed up" message.
503|The service is currently unavailable, it usually means that the server is just temporarily down.
504|Gateway timeout, the connection to the server timed out.
