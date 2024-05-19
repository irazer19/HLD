#### API vs Endpoint:
APIs and endpoints are two different entities. An API is the method by which two software applications communicate, and an 
endpoint is a component of the API. Endpoints define the exact location of the available resources. In contrast, API uses 
these endpoint URLs to make its resources available to its users. <br/>

#### OSI model:
1. Application layer: The sender interacts with the application layer, and it includes different protocols, for example, HTTP and SMTP protocols.
2. Presentation layer: t takes care of the data's format on the sender and receiver sides. It ensures the data is understandable at the receiver end. Also, it may perform encryption, decryption, and compression of the data.
3. Session layer: It creates, manages, and terminates the sessions between end-to-end devices. It’s also responsible for authentication and reconnections.
4. Transport layer: It’s responsible for data ordering, reliability, and error checking. Example: TCP, UDP
5. Network layer: IP addressing and routing is the responsibility of the network layer. A node connected to the internet needs to have an IP address for communication with peers.
6. Data link layer: This layer is responsible for frame transmission, address for local area network (LAN), and logical link control. In OSI models, the data unit is considered to be a packet in the network layer and a frame in the data link layer.
7. Physical layer: It handles the transmission of bitstreams on the physical link between the sender and the immediate next hop receiver. The physical link can be Ethernet, DSL, and so forth.

Latency means how long (in terms of time) a user-level message takes to travel from the sender to the receiver.<br/>
Variation in latency is called jitter. It’s the measure of how latency changes from one packet to the next.<br/>

A socket is an interface that creates a two-way channel between processes communicating on different devices. Processes running 
on the application layer use sockets as an interface to take services from the transport layer to establish communication. 
Further, the interfacing requires an IP address and a port number to uniquely identify a process or application globally. 
The interface (IP address + port) is referred to as a socket address. <br/>

Network sockets can be categorized into two general types based on the transport protocol.
1. Stream Sockets: A stream socket creates a reliable end-to-end connection between the two endpoints using transport protocols like TCP and SCTP to transmit data between processes. It also utilizes the recovery facility of the underlying protocol (for example, TCP) to retransmit the lost data during the data propagation phase.
2. Datagram Sockets: Unlike stream sockets, datagram sockets don’t create an end-to-end channel between two endpoints to transfer data between processes. It just sends data and expects it to reach the receiver end. It’s used in scenarios where data loss is not significant. It usually operates on a UDP-like protocol for data transfer.

The Internet is a network of networks with a series of interconnected nodes that can communicate with each other. 
In contrast, the web is one of the applications built on the Internet. <br/>

Resources over the Internet are identified using a Uniform Resource Identifier (URI). The URI consists of three parts:
1. Protocol: The HTTPS protocol is used to fetch the web page.
2. Domain name: The DNS name shows where the web page is located.
3. Unique path: The unique path determines the web page that needs to be accessed within a domain.

The primary difference between HTTP/2.0 and HTTP/3.0 is the transport protocol that is used to support HTTP messages. 
The previous version relied on the Transmission Control Protocol (TCP). However, HTTP/3.0 utilizes QUIC (Quick UDP Internet Connections) on top of User Datagram Protocol (UDP) <br/>

### Remote Procedure Call (RPC):
A Remote Procedure Call (RPC) is an interprocess communication technique used in client-server based applications to enable a 
program to execute a procedure (or function) on a remote server as if it were a local call. <br/>
The client should know the ip_address and port of the server for establishing the connection.

Steps in RPC:
1. Client Stub: The client calls a local stub procedure, which packages the parameters into a message (marshalling) and sends it to the server.
2. Transport Layer: The message is transmitted over the network to the server.
3. Server Stub: The server receives the message, unpacks the parameters (demarshalling), and calls the actual procedure.
4. Execution and Return: The procedure executes on the server, and the results are sent back to the client in a similar manner13.

Example: 
In gRPC .proto is a file that defines the structure of the data and the services used in gRPC communication.
It uses Protocol Buffers (protobuf), which is a language-neutral, platform-neutral, extensible mechanism for serializing structured data.
It is used to generate the necessary client and server code, enabling efficient and structured remote procedure calls.<br/>

### Websockets:
WebSocket was introduced in 2011 to enable full-duplex asynchronous communication over a single TCP connection to use resources efficiently. 
HTTP connection restricts TCP to a one-sided communication, where the client always starts the communication due to the request-response model. 
In other words, the client first sends requests, then the server responds to them, which is a half-duplex communication. 
In contrast, WebSockets take full advantage of the TCP connection allowing clients and servers to send or receive data on demand. 
WebSocket is a protocol that allows web applications to communicate bidirectionally over a single TCP connection.<br/>

A WebSocket establishes an HTTP connection and then upgrades it to the WebSocket protocol. All the transmission happens directly on the TCP channel. 
The URLs for connections using WebSocket begin with ws:// and wss:// for non-TLS and TLS-based connections, respectively. <br/>

Data exchange format for an API depends on the need.
Example:
1. Text based format: JSON is probably the ideal choice when dealing with small groups of systems, especially those developed in JavaScript, where human-readability is essential.
2. Binary data format: Protobuf or Thrift may serve the purpose when network latency, interprocess communication, and processing speed are paramount.

#### Various API Architecture Style:
1. REST
2. RPC
3. GraphQL

#### REST API best practices:
1. Avoid using verbs and use nouns in the endpoint, Ex: Instead of /getUser, use /user
2. Use standard HTTP error codes regularly when an error occurs.
3. Use Filtering and pagination.
4. Implement security practices
5. API versioning
6. API documentation

#### GraphQL vs REST API:
Problems with REST API:
1. Clients often need to make multiple round-trips to different endpoints to gather all the required data. This can lead to over-fetching, where clients receive more data than needed, wasting network and memory resources.
2. Clients have limited control over the data returned by the server. They cannot specify which fields to retrieve, leading to either over-fetching or under-fetching of data.

Solution using GraphQL:
1. Allows clients to request exactly the data they need in a single query, reducing the number of round-trips and preventing over-fetching.
2. Clients can specify exactly which fields they need, providing more flexibility and efficiency in data fetching.

GraphQL is sometimes confused with the database, but it’s actually a query language for APIs. <br/>
The implementation of GraphQL can be divided into two components: 
1. GraphQL server
2. GraphQL client: Actual front-end component that allows us to accept queries, connect to the GraphQL endpoint, and issue queries to gather data

GraphQL server contains: 
1. Schema: A schema is a model of the data and defines relationships between the data. Based on the schema, the server specifies what types of queries and data a client can request. 
2. Resolve functions: A schema can tell us what types of data a client can request but lacks information about where the data comes from. Here, the resolve functions specify how types and fields in the schema are connected to various backends.

GraphQL mutations: We can think of GraphQL mutations as the equivalent of POST, PUT, PATCH, and DELETE methods used by REST. <br/>
Example: 
1. Insert mutations: These are used to insert a new record on the server side.
2. Update mutations: These are used to modify an existing record in the database.
3. Delete mutations: These are used to delete a specific record from the database.

#### GraphQL request format:
```text
query{
    starship(starshipID:10) {
       name
       length
  	   cargoCapacity
       }
}
```

#### GraphQL response format:
```text
{
  "data": {
     "starship": {
        "name": "Millennium Falcon",
        "length": 34.37,
        "cargoCapacity": 100000
    }
  }
}
```

### gRPC:
gRPC is an RPC framework that achieves high performance by leveraging the multiplexing functionality to create logical subchannels to support the following types of connections:
1. Request-response: The client can send a single request, and the server can reply with a single response.
2. Client streaming: The client can send multiple requests, and the server can reply with a single response.
3. Server streaming: The client can send a single request, and the server can reply with multiple responses.
4. Bidirectional streaming: The client can send multiple requests, and the server can reply with multiple responses.

In gRPC, Protobuf is the default interface definition language (IDL). <br/>
gRPC Channel vs Subchannel: A channel is the actual TCP connection created between a gRPC client and a gRPC server. A subchannel is the logical management of HTTP/2 streams inside this channel. <br/>
Every response returned by the server ends with trailing metadata, which is important for load balancers because it carries information about the availability and load on the server. <br/>
The gRPC framework provides more control over the HTTP protocol, allowing it to adjust data transfer rates based on client capabilities, which is why it can be considered a better choice when dealing with resource-constrained devices. <br/>

#### When to use REST API?
1. When CRUD operation is needed.
2. Stateless behavior in the request & response.

#### When to avoid REST API?
1. When there is a need for event-driven architecture.
2. Complex query requirements.

#### When to use GraphQL?
1. When there is a client application gathering data from multiple data sources. GraphQL aggregates data from multiple data sources and sends a consolidated response to the client.
2. When applications can ask for the specific fields they want to present to the user instead of requesting all the fields.

#### When to avoid GraphQL?
1. GraphQL is not the right option for server-to-server communication. For example, if we want to build a way for some back-end services to speak to each other, GraphQL might not be a good choice here

#### When to use gRPC?
1. If we have to design a low-latency, highly scalable distributed system, we should consider gRPC.
2. If we aim to build a back-end system including an enormous number of interconnected microservices. In such a case, gRPC can provide efficiency and speed.

#### When to avoid gRPC?
1. If the developer's or consumer’s language is not supported by the framework.
2. In applications if they are calling a limited number of back-end services, it's best to use REST for ease.

### API Security:
To guarantee that a certain security goal is met, we apply the following mechanisms:
1. Encryption
2. Validation
3. Authentication
4. Authorization

Transport layer security (TLS) is a cryptographic protocol that permits safe transmission between the client and API provider. TLS ensures message authentication, encryption, and data integrity. <br/>
#### Steps in TLS handshake:
1. Client Hello: The client initiates the handshake by sending a "Client Hello" message to the server. This message includes the client's supported TLS version, cipher suites, compression methods, and a random string called the "client random".
2. Server Hello: The server responds with a "Server Hello" message. This message contains the server's chosen TLS version, cipher suite, compression method, and a random string called the "server random". The server also sends its digital certificate to the client for authentication.
3. Server Authentication and Key Exchange: The server sends its digital certificate to the client, which includes the server's public key. The server then sends a "Server Hello Done" message to indicate it has finished its part of the handshake.
4. Client Authentication and Premaster Secret: The client verifies the server's certificate with a trusted Certificate Authority (CA). If the server requests client authentication, the client sends its certificate. The client then generates a premaster secret, encrypts it with the server's public key, and sends it to the server in a "Client Key Exchange" message.
5. Decryption and Master Secret Generation: The server decrypts the premaster secret using its private key. Both the client and server then use the premaster secret, along with the client random and server random, to generate the master secret. This master secret is used to create session keys for encryption and decryption.
6. Change Cipher Spec and Finished Messages: The client sends a "Change Cipher Spec" message to inform the server that it will start using the newly negotiated encryption keys. The client then sends a "Finished" message, encrypted with the session key, indicating that the client part of the handshake is complete.
7. The server responds with its own "Change Cipher Spec" message and a "Finished" message, also encrypted with the session key, indicating that the server part of the handshake is complete.
8. Secure Communication: After the handshake is complete, the client and server use the session keys to encrypt and decrypt the data they exchange, ensuring secure communication.

How does the client know that the server it’s talking to is exactly the one the client intended? <br/>
Through the use of digital certificates, the client and server are identified. <br/>
How do we achieve confidentiality/secrecy of the messages? <br/>
Confidentiality is achieved with the encryption protocols implemented because even if an attacker intercepts a transmission, they won't be able to comprehend or decrypt the ciphertext. <br/>

#### Input validations:
1. Client side validation: Mostly at the browser side.
2. Server side validation: Has multiple checks and data sanity test.

#### Cross-Origin Resource Sharing (CORS):
Suppose that John is lured into visiting www.evil-site.com. This site responds with JavaScript code that then makes a call to www.facebook.com, where 
John logs in without any hesitation. As a consequence, the JavaScript code downloaded from www.evil-site.com obtains access to the DOM elements of 
www.facebook.com and, and to John's sensitive data. <br/>

The example that we saw above demonstrates an unrestricted interaction between two web pages belonging to different origins, which could lead to a potential data breach. 
An origin is defined as a combination of scheme (protocol), hostname, and port number. <br/>
To solve the above problem, Same-origin-policy (SOP) was created, which only allows access to resources which are coming from the same origin. 
But it's too restrictive for many apps that want to access resource from different origin, so CORS was made. <br/>

CORS allows two types of cross-origin requests: <br/>
Simple: The process begins with a cross-origin request initiated by http://abc.com for data stored in the http://xyz.com server. 
In this example, while http://abc.com is a web service, in our context, it will act as a client. The request contains the client's Origin. 
A response is then sent from the server to the browser. The server adds an Access-Control-Allow-Origin header to the response. 
The browser then compares the Origin in the client's request with Access-Control-Allow-Origin in the server's response. If they are identical, the cross-origin request is permitted. <br/>

Preflighted: A preflight request is a mechanism used in Cross-Origin Resource Sharing (CORS) to ensure the safety and permission of complex HTTP 
requests before they are sent to the server. A preflight request is an HTTP OPTIONS request sent by the browser to the server before the actual request. It checks if the server permits 
the actual request based on the specified HTTP method and headers. <br/>

Authentication in preflight requests:
To enable this, we must manually specify the flag withCredentials = true for the request. 
The Access-Control-Allow-Credentials header in the server's response must also be set as true. <br/>

### Authentication & Authorization:
1. Authentication refers to the procedure through which our API verifies who the user is.
2. Authorization is controlling what the user has access to.

#### HTTP basic authentication:
HTTP basic authentication is a rudimentary scheme that verifies a client through username and password authentication. 
It encodes the user's username and password in Base64 and embeds it into its Authorization header. <br/>

#### API keys:
API keys deal with the shortcomings of HTTP basic authentication by replacing the encoded username and password with a generated string.
With API key authentication, the application forwards its assigned API key in the header of its request. When the server receives the said request, 
it looks up the API key in its database in hopes of verifying the application. Because the API is separate from the user’s username and password, any security breach will be limited to the API. <br/>
Disadvantage: Need another authorization protocol alongside them, or else attackers can gain access to API keys and subsequent permissions. <br/>

#### JSON Web Token (JWT):
A JSON Web Token (JWT) is an open standard that’s a compact and self-sufficient method for safely transferring data between entities in the form of JSON objects. 
JWTs are a collection of encrypted strings denoting a header, a payload, and a signature that travel through HTTP requests. Unlike the previous protocols, 
tokens can be used for both authentication and authorization purposes because they carry information about the token's holder. <br/>

JSON Web Tokens (JWTs) are composed of three main parts:
1. Header: The header typically consists of two parts: Type of the token: This is usually "JWT". Signing algorithm: This specifies the algorithm used to sign the token, such as HMAC SHA256 or RSA.
2. Payload: The payload contains the claims, which are statements about an entity (typically, the user) and additional metadata.
3. Signature: The signature is used to verify the token's integrity and authenticity. It is created by taking the encoded header, the encoded payload, a secret, and the algorithm specified in the header, and then signing them.

A complete JWT looks like this: xxxxx.yyyyy.zzzzz, where xxxxx is the Base64Url encoded header, yyyyy is the Base64Url encoded payload, and zzzzz is the signature. <br/>

#### API keys and tokens may seem similar, but there are a few key differences:
1. API keys only serve to identify the client, whereas tokens carry more information with them, such as their source, the identifier, and other metadata. This extra information is helpful for authorization purposes.
2. Tokens are structured to contain a header and a payload. API keys are just generated strings.

#### Steps using jwt:
1. The user provides their credentials (e.g., username and password) to the authentication server.
2. The server checks the credentials. If they are correct, the server generates a JWT.
3. The server sends the JWT to the client (e.g., web browser). The client stores the JWT, typically in local storage or a cookie.
4. For subsequent requests to protected resources, the client includes the JWT in the HTTP Authorization header using the Bearer schema: Authorization: Bearer <token>.
5. The server verifies the JWT by checking the signature and ensuring the token has not expired and is valid.
6. Server grants or denies access based on the JWT's validity.








