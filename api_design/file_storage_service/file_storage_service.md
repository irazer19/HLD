# Cloud Storage Service like AWS S3

### Functional requirements:
1. Upload: The API should allow users to securely upload files to remote storage.
2. Download: The API should allow users to download the uploaded files from remote storage.
3. Delete: The API should allow only the file owners to delete uploaded files from remote storage.
4. List: The API should allow file owners to list uploaded files in remote storage.

### Non-functional requirements:
1. Reliability: Data should not be lost or corrupted during the transfer (during upload and download operations). Additionally, data must be stored persistently after a successful upload.
2. Security: The API should adopt appropriate security mechanisms to provide secure access to data.
3. Scalability: The API should be scalable to handle the increasing number of users and files.
4. Availability: The API should have high availability, allowing users to upload/download data on demand.
5. Low latency: The API should be able to upload/download data with low latency.

### Some components:
1. File servers:
    1. Accept and process file API requests forwarded by the API gateway
    2. Split requests into metadata (user and file information) and file content.
2. Processing server:
    1. Performs encoding/decoding of data into different encoding schemes
    2. Encrypt/decrypt data at-rest to prevent unauthorized access
3. User to file mapping system (UFMS): Maps users to files and where those files can be found in storage
4. Temporary storage: Stores files and objects temporarily before processing

#### API protocol:
We should use REST because it has better support for different operations in our file API and avoids unnecessary complexity. <br/>
Therefore, we propose REST as a communication protocol from client to API gateway and from API gateway to downstream services. <br/>

#### Data format:
JSON provides everything we need and is also suitable for the RESTful API style. So, JSON is the data exchange format from client to API gateway and from API gateway to downstream services. <br/>
The actual file content is transmitted in binary format. Only the requests and responses are formatted in JSON for processing. <br/>

#### Base URL and API endpoints:
https://api.example.com/v1.0/files <br/>

The API will make use of these fields while performing different functions:
```text
type file
{
    fileId: string      // Unique identifier of a file on the host system
    ownerId: string     // Unique identifier of a user on the host system
    authToken: string   // Token verifying the authenticity and privileges of the user
    checksum: string    // Hash value verifying the integrity of data
    fileLink: string    // The URI of the stored the file contents
    userList: list      // A list of users with the specified permissions to access the resource
    timeStamp: date     // The data and time at which the particular file is uploaded
    fileTitle: string   // The name/title of the file along with its extension
    fileSize: long      // Total size of a file in bytes
    content: binary     // The actual content of a file being transferred
    mimeType: *         // file format or extension of the file such as png, jpeg, mp3, mkv, etc.
}
```
#### Upload File Request format:
```http request
POST /v1.0/files HTTP/1.1
HOST: api.example.com
Authorization: Bearer <JWT>
Content-Type: multipart/mixed;boundary={---xxBOUNDARYxx---}
Content-Length: xyz
{
   body
}
```
Note that the Content-Type in the header above is set to multipart/mixed, which means that this request contains different parts, and each part can have 
a different encoding type (JSON or binary). We send the information related to the file (metadata) as JSON for ease of processing, while the actual file 
content is transmitted in binary. The placeholder {---xxBOUNDARYxx---} is a randomly generated bounding string that surrounds each such section. <br/>

#### Upload file response format:
```http request
HTTP/1.1 200 OK
Content-Length: xyz
Content-Type: application/json
{
    timestamp
    file_id
}
```

#### List uploaded files request format:
```http request
GET /v1.0/files HTTP/1.1
HOST: api.example.com
Authorization: Bearer <JWT>
Accept: application/json
```

#### List uploaded files response format:
```http request
HTTP/1.1 200 OK
Content-Length: xyz
Content-Type: application/json
{
    "files":[
        "fileTitle": "/files/{fileId}"
        ... 
    ]
}
```

#### Download file request format:
```http request
GET /v1.0/files/{fileId} HTTP/1.1
HOST: api.example.com
Authorization: Bearer <JWT>
Accept: */*
```

#### Download file response format:
```http request
HTTP/1.1 200 OK
Content-Length: xyz
Content-Type: */*
{
    body
}
```
The server may also respond with a link to download the file from a CDN:
```http request
HTTP/1.1 302 Found
Location: "cdn.provider.com/files/{fileId}"
```

Most cloud storage services handle the upload/download of large files in chunks. The download/upload manager at client-end prepares the chunks and handles
resumable downloads/uploads.