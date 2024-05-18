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

