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

