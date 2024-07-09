# HTTP (HyperText Transfer Protocol)

HTTP is a protocol used for transferring hypertext documents, such as HTML. It allows different systems to communicate over the internet.

HTTP follows a client-server model. The client, typically a web browser, sends a request to the server, and the server processes this request and sends back a response.

HTTP operates over TCP (Transmission Control Protocol), which provides a reliable, ordered, and error-checked delivery of data between applications running on hosts communicating via an IP network.

## HTTP Request and Response

## Request

An HTTP request is composed of several parts:

*Request Line*: This line contains the HTTP method, the resource URI, and the HTTP version. `GET /index.html HTTP/1.1`

*Headers*: These are key-value pairs that provide additional information about the request.

Example:
```
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

*Blank Line*: A blank line indicates the end of the headers section.

*Body*: This is optional and used primarily with methods like POST and PUT to send data to the server. For GET requests, the body is usually empty.

Example (for a POST request):
```
{
  "username": "example",
  "password": "password123"
}
```

## Response

An HTTP response is also composed of several parts:

*Status Line*: This line contains the HTTP version, a status code, and a reason phrase.

Example: `HTTP/1.1 200 OK`

*Headers*: These are key-value pairs that provide additional information about the response.

Example:
```
Content-Type: text/html
Content-Length: 138
Server: Apache/2.4.1 (Unix)
```

*Blank Line*: A blank line indicates the end of the headers section.

*Body*: This contains the data requested by the client, such as an HTML document, image, or JSON response.

Example:
```
<html>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```

## Methods

- GET: Requests data from a specified resource.
- POST: Submits data to be processed to a specified resource.
- PUT: Updates or creates a resource at a specified URI.
- DELETE: Deletes the specified resource.
- HEAD: Similar to GET but only retrieves the headers.
- OPTIONS: Describes the communication options for the target resource.
- PATCH: Applies partial modifications to a resource.

## Resources

In the context of HTTP, a resource is any content that can be identified and accessed via the web. This includes:

- HTML documents: Web pages.
- Images: JPEG, PNG, GIF files.
- Videos: MP4, AVI files.
- APIs: JSON or XML data endpoints.
- Scripts: JavaScript files.
- Stylesheets: CSS files.
- Each resource is identified by a *URI* (Uniform Resource Identifier).

## URI vs URL vs URN

*URI (Uniform Resource Identifier)*
A URI is a string that identifies a resource either by location, name, or both. It is a generic term that includes both URLs and URNs.
Example: `http://www.example.com/index.html`

*URL (Uniform Resource Locator)*
A URL is a specific type of URI that not only identifies a resource but also provides a means of locating it by describing its primary access mechanism (e.g., its network location).

Example: `http://www.example.com/index.html`
Scheme: `http` (indicates the protocol).
Host: `www.example.com` (indicates the domain name).
Path: `/index.html` (indicates the specific resource on the host).

Differences
- All URLs are URIs, but not all URIs are URLs.
- A URI can be a URL (which specifies the location and access method) or a URN (which names the resource without specifying the location or access method).
- URL: Contains the protocol, domain, and path to the resource.
- URI: A more general identifier, can be a URL or just a name (URN). An example of a URN is the ISBN number of a book.


A URI (Uniform Resource Identifier) can be broken down into several components:

- Scheme: Indicates the protocol (e.g., http, https, ftp, ssh, ...).
- Authority: Composed of the user information, host, and port (e.g., user:password@host:port).
  - Default ports: 80 `http`, 443 `https`, 21 `ftp`, 22 `ssh`, ...
- Path: Specifies the resource location (e.g., /path/to/resource).
- Query: Contains query parameters (e.g., ?key1=value1&key2=value2).
- Fragment: Indicates a specific part of the resource (e.g., #section1).
Example URI: https://user:password@www.example.com:8080/path/to/resource?key1=value1&key2=value2#section1

## Common Headers

Request headers:
- Host: Specifies the domain name of the server (for virtual hosting), and optionally the port number. `Host: www.example.com`
- User-Agent: Contains information about the user agent (browser) originating the request. `User-Agent: Mozilla/5.0`
- Accept: Informs the server about the types of data that can be sent back. `Accept: text/html,application/xhtml+xml`
- Content-Type: Indicates the media type of the resource sent to the server. `Content-Type: application/json`
- Authorization: Contains credentials for authenticating the client with the server. `Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l`

Response headers:
- Content-Type: Indicates the media type of the resource. `Content-Type: text/html; charset=UTF-8`
- Content-Length: Indicates the size of the response body in bytes. `Content-Length: 348`
- Set-Cookie: Sends cookies from the server to the client. `Set-Cookie: sessionId=abc123; HttpOnly`
- Cache-Control: Directives for caching mechanisms in both requests and responses. `Cache-Control: no-cache`
- Server: Contains information about the server software handling the request. `Server: Apache/2.4.1 (Unix)`

## Common Status Codes

HTTP status codes are three-digit numbers that indicate the result of the HTTP request. They are grouped into five categories based on the first digit:

- 1xx: Informational
- 2xx: Success
- 3xx: Redirection
- 4xx: Client Errors
- 5xx: Server Errors

Informational
- 100 Continue: The server has received the request headers, and the client should proceed to send the request body.
- 101 Switching Protocols: The requester has asked the server to switch protocols, and the server has agreed to do so.

Success
- 200 OK: The request has succeeded. The meaning of the success depends on the HTTP method:
	GET: The resource has been fetched and is transmitted in the message body.
	POST: The resource describing the result of the action is transmitted in the message body.
- 201 Created: The request has been fulfilled, and a new resource has been created.
- 202 Accepted: The request has been accepted for processing, but the processing is not complete.
- 204 No Content: The server successfully processed the request, but there is no content to send in the response body.

Redirection
- 301 Moved Permanently: The resource requested has been permanently moved to a new URL.
- 302 Found: The resource requested is temporarily available at a different URL.
- 303 See Other: The response to the request can be found under a different URL and should be retrieved using a GET method.
- 304 Not Modified: The resource has not been modified since the version specified by the request headers. The client can use the cached version.
- 307 Temporary Redirect: The resource requested is temporarily available at a different URL and should be accessed using the same HTTP method.

Client Errors
- 400 Bad Request: The server cannot or will not process the request due to a client error (e.g., malformed request syntax).
- 401 Unauthorized: The request requires user authentication.
- 403 Forbidden: The server understood the request but refuses to authorize it.
- 404 Not Found: The server cannot find the requested resource.
- 405 Method Not Allowed: The method specified in the request is not allowed for the resource identified by the request URI.
- 409 Conflict: The request could not be completed due to a conflict with the current state of the resource.
- 429 Too Many Requests: The user has sent too many requests in a given amount of time ("rate limiting").

Server Errors
- 500 Internal Server Error: The server encountered an unexpected condition that prevented it from fulfilling the request.
- 501 Not Implemented: The server does not support the functionality required to fulfill the request.
- 502 Bad Gateway: The server, while acting as a gateway or proxy, received an invalid response from the upstream server.
- 503 Service Unavailable: The server is currently unable to handle the request due to temporary overloading or maintenance.
- 504 Gateway Timeout: The server, while acting as a gateway or proxy, did not receive a timely response from the upstream server.
- 505 HTTP Version Not Supported: The server does not support the HTTP protocol version used in the request.

These status codes help in understanding the outcome of the HTTP requests and in debugging issues with web applications.

# HTTPS (HTTP Secure)

HTTPS is HTTP with encryption. It uses TLS (Transport Layer Security) or SSL (Secure Sockets Layer) to encrypt the data being transmitted between the client and server, ensuring:

- Confidentiality: Data is encrypted, so eavesdroppers cannot read it.
- Integrity: Data cannot be altered without detection.
- Authentication: Confirms the identity of the website (prevents man-in-the-middle attacks).

# HTTP/2 and HTTP/3

HTTP/2 is a major revision of the HTTP/1.1 protocol and offers several improvements:

- Multiplexing: Multiple requests and responses can be sent over a single TCP connection.
- Header Compression: Reduces the overhead of HTTP headers.
- Stream Prioritization: Allows clients to prioritize resource loading.
- Server Push: Enables the server to send resources to the client proactively.

HTTP/3 is the latest version of the HTTP protocol and runs over QUIC (Quick UDP Internet Connections):

- Uses UDP instead of TCP: Provides faster connection establishment.
- Built-in Encryption: Always encrypted, enhancing security.
- Improved Performance: Reduces latency and improves connection reliability, especially on mobile networks.

# REST

## What is REST

REST (Representational State Transfer) is an architectural style for designing networked applications. It relies on a stateless, client-server communication protocol, typically HTTP. RESTful services are designed around resources, which are identified by URLs.

Key Principles of REST
- Statelessness: Each request from the client to the server must contain all the information needed to understand and process the request. The server does not store any state about the client session on the server side.
- Client-Server Architecture: The client and server operate independently, allowing them to evolve separately.
- Cacheability: Responses must define themselves as cacheable or not to prevent clients from reusing stale or inappropriate data.
- Uniform Interface: A consistent and uniform interface simplifies and decouples the architecture, which allows each part to evolve independently.
- Layered System: The architecture can be composed of multiple layers, where each layer has a specific functionality, improving scalability and manageability.
- Code on Demand (Optional): Servers can temporarily extend or customize client functionality by transferring executable code.

## JSON

JSON (JavaScript Object Notation) is a lightweight data interchange format that is easy for humans to read and write and easy for machines to parse and generate.

## How REST/JSON Uses HTTP/HTTPS

- RESTful services use standard HTTP methods to perform operations on resources. `GET, POST, ...`
- Resource Identification: Resources are identified by URIs. `http://api.example.com/users/123`
- Stateless Communication: Each request is self-contained and independent. All necessary information to process the request is included in the HTTP headers, URI, and body.
- HTTP Headers: RESTful APIs use standard HTTP headers to convey metadata:
  - Content-Type: Indicates the media type of the resource `application/json`
  - Accept: Informs the server about the types of data that can be sent back. `application/json`
  - Authorization: Used for authentication. `Bearer <token>`
- Response Codes: Standard HTTP status codes are used to indicate the outcome of the request.

## Examples

Request: Get user with id 123
```
GET /users/123 HTTP/1.1
Host: api.example.com
Accept: application/json
Authorization: Bearer your_access_token`
```

Response: 
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 85

{
  "id": 123,
  "name": "John Doe",
  "email": "johndoe@example.com"
}
```

# Advanced Topics

## Caching

Caching is crucial for improving performance and reducing latency. Key HTTP headers for caching include:

- Cache-Control: Directs caching mechanisms (e.g., no-cache, no-store, max-age=3600).
- Expires: Provides a date/time after which the response is considered stale.
- ETag: A unique identifier for a specific version of a resource, used for cache validation.
- Last-Modified: Indicates when the resource was last modified.

## Content Negotiation

HTTP allows clients to specify their preferred format for responses using headers:

- Accept: Specifies media types (e.g., Accept: application/json).
- Accept-Language: Specifies language preferences (e.g., Accept-Language: en-US).
- Accept-Encoding: Specifies acceptable encodings (e.g., Accept-Encoding: gzip).

## Cross-Origin Resource Sharing (CORS)

CORS is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served.
Key headers include:

- Origin: Indicates the origin of the request.
- Access-Control-Allow-Origin: Specifies which origins are permitted to access the resource.
- Access-Control-Allow-Methods: Lists HTTP methods allowed when accessing the resource.
- Access-Control-Allow-Headers: Lists headers allowed when accessing the resource.


## Security Headers

Security headers help protect against various attacks:

- Content-Security-Policy (CSP): Helps prevent cross-site scripting (XSS) attacks.
- Strict-Transport-Security (HSTS): Ensures that browsers only communicate with the server over HTTPS.
- X-Content-Type-Options: Prevents MIME type sniffing.
- X-Frame-Options: Protects against clickjacking attacks.
- X-XSS-Protection: Enables cross-site scripting filters in browsers.