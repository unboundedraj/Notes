---
title: API
date: 2026-11-01
tags: [api]
---

# Introduction

An API (Application Programming Interface) is a set of rules that allows different software applications to communicate with each other. It provides a structured way for one application to request data or functionality from another application.  
An API acts as an interface between a client and a server, allowing them to communicate and exchange data. It receives a request from the client, processes it, and returns an appropriate response.

## What is an API, and how does an API work internally?

An API (Application Programming Interface) allows two software applications to communicate with each other through a defined set of rules and endpoints.

How it works:

1. Client sends an HTTP request to an API endpoint.
2. Server receives and validates the request.
3. Business logic is executed.
4. Server interacts with the database or other services if required.
5. Server returns an HTTP response with a status code and data, usually in JSON format.

```
GET /api/users/101 HTTP/1.1
Host: example.com
Accept: application/json

// RESPONSE JSON:
{
  "id": 101,
  "name": "John",
  "email": "john@example.com"
}
```

## What is the difference between REST, SOAP, GraphQL, and gRPC?

These are different approaches or technologies used for communication between applications.


| Feature       | REST                | SOAP                   | GraphQL                 | gRPC             |
| ------------- | ------------------- | ---------------------- | ----------------------- | ---------------- |
| Type          | Architectural style | Protocol               | Query language          | RPC framework    |
| Data format   | Usually JSON        | XML                    | Usually JSON            | Protocol Buffers |
| Transport     | HTTP                | HTTP and others        | Usually HTTP            | HTTP/2           |
| Communication | Resource-based      | Operation-based        | Query-based             | Procedure-based  |
| Performance   | Good                | Relatively heavyweight | Efficient data fetching | High performance |


Key differences:

- REST: Uses HTTP methods such as GET, POST, PUT, and DELETE.
- SOAP: Uses XML-based messages and strict communication standards.
- GraphQL: Allows clients to request exactly the data they need.
- gRPC: Uses Protocol Buffers for compact serialization and efficient communication, particularly between microservices.

## What are the key principles and constraints of REST architecture?

REST (Representational State Transfer) is an architectural style for designing network-based applications.

It follows six main constraints:

1. Client-Server: Client and server operate independently.
2. Stateless: Every request must contain the information needed to process it. The server does not rely on previous request context.
3. Cacheable: Responses should indicate whether they can be cached.
4. Uniform Interface: Consistent resource identification and interaction through standard methods.
5. Layered System: Client doesn't need to know whether it communicates directly with the server or through intermediaries.
6. Code on Demand (Optional): Server can optionally send executable code to the client.

```
// Example of resource-based endpoints:
GET    /api/users
GET    /api/users/101
POST   /api/users
PUT    /api/users/101
DELETE /api/users/101
```

## What is the difference between REST API and RESTful API?

A REST API is an API designed using REST architectural concepts, whereas a RESTful API strictly follows the REST architectural constraints.

In practice, the terms are often used interchangeably.

Example:

A REST-style API might use:

```
GET /getUser?id=101
```

A more RESTful approach would be:

```
GET /users/101
```

The second approach identifies a resource using a URI and uses HTTP methods to define the operation.

## What is the difference between synchronous and asynchronous APIs?

Synchronous API: The client sends a request and waits for the server to complete processing and return a response.

Asynchronous API: The client initiates an operation without necessarily waiting for it to finish. The result can be communicated later through polling, webhooks, callbacks, or messaging systems.


| Synchronous Application Programming Interface | Asynchronous Application Programming Interface |
| --------------------------------------------- | ---------------------------------------------- |
| Client waits for response                     | Client need not wait                           |
| Immediate response expected                   | Result may arrive later                        |
| Suitable for simple operations                | Suitable for long-running operations           |
| Simpler request-response flow                 | Requires additional coordination               |


## Explain the different HTTP methods: GET, POST, PUT, PATCH, and DELETE.


| Method | Purpose                                   | Example             |
| ------ | ----------------------------------------- | ------------------- |
| GET    | Retrieve data                             | Get user details    |
| POST   | Create a resource or trigger an operation | Create a user       |
| PUT    | Replace a resource completely             | Update user details |
| PATCH  | Partially update a resource               | Update user email   |
| DELETE | Delete a resource                         | Delete a user       |


```
GET /users/101
POST /users
PUT /users/101
PATCH /users/101
DELETE /users/101
```

Important interview point: GET is a safe and idempotent method. PUT and DELETE are also idempotent, whereas POST is generally neither safe nor idempotent.

## What is the difference between HTTP status codes 200, 201, 202, and 204?

These status codes indicate successful processing of an HTTP request.


| Status         | Meaning                              | When to use               |
| -------------- | ------------------------------------ | ------------------------- |
| 200 OK         | Request successful                   | Fetching or updating data |
| 201 Created    | Resource successfully created        | Creating a new user       |
| 202 Accepted   | Request accepted for processing      | Background processing     |
| 204 No Content | Request successful, no response body | Successful deletion       |


## Explain the difference between 400, 401, 403, 404, and 405.


| Status | Meaning            | Explanation                                          |
| ------ | ------------------ | ---------------------------------------------------- |
| 400    | Bad Request        | Invalid request syntax or parameters                 |
| 401    | Unauthorized       | Missing or invalid authentication credentials        |
| 403    | Forbidden          | Authenticated user lacks permission                  |
| 404    | Not Found          | Requested resource doesn't exist or is not disclosed |
| 405    | Method Not Allowed | HTTP method isn't supported for that resource        |


## What are HTTP headers? Explain commonly used request and response headers.

HTTP headers provide additional information about an HTTP request or response. They communicate metadata such as content format, authentication credentials, caching instructions, and server information.

Common request headers:


| Header        | Purpose                               |
| ------------- | ------------------------------------- |
| Accept        | Specifies acceptable response formats |
| Content-Type  | Specifies request body format         |
| Authorization | Contains authentication credentials   |
| User-Agent    | Identifies the client                 |
| Cookie        | Sends stored cookies                  |
| Cache-Control | Specifies caching directives          |


Common response headers:


| Header                      | Purpose                                       |
| --------------------------- | --------------------------------------------- |
| Content-Type                | Specifies response body format                |
| Set-Cookie                  | Sets cookies in the browser                   |
| Cache-Control               | Controls response caching                     |
| ETag                        | Identifies a specific resource representation |
| Location                    | Specifies resource or redirect location       |
| Access-Control-Allow-Origin | Specifies permitted CORS origins              |


## What is the difference between path parameters, query parameters, and request body parameters?

These are different ways of passing information to an API.

1. Path Parameters: Used to identify a specific resource.

```
GET /users/101
```

Here, `101` is the path parameter.

2. Query Parameters: Used for filtering, sorting, searching, and pagination.

```
GET /users?role=admin&page=2&limit=10
```

Here, `role`, `page`, and `limit` are query parameters.

3. Request Body Parameters: Used to send structured data, commonly with POST, PUT, and PATCH.

```
POST /users
Content-Type: application/json
```

```
{
  "name": "John",
  "email": "john@example.com"
```

Interview tip: Path parameters identify resources, query parameters modify the result set, and body parameters provide data for processing.

## What is the difference between cookies, sessions, and tokens?


| Feature           | Cookies                  | Sessions              | Tokens                          |
| ----------------- | ------------------------ | --------------------- | ------------------------------- |
| Storage           | Browser                  | Usually server-side   | Client-side                     |
| Purpose           | Store client data        | Maintain user session | Authenticate/authorize requests |
| Server dependency | Depends on usage         | Usually required      | Can be stateless                |
| Common usage      | Browser preferences/auth | Traditional web login | REST API authentication         |


Cookies: Small pieces of data stored by the browser and automatically sent with matching requests.

Sessions: Server maintains user-specific information and provides a session ID, usually stored in a cookie.

Tokens: Credentials issued by an authentication system and sent with requests, commonly through the Authorization header.

> Important: Cookies are a storage and transport mechanism, while sessions and tokens are mechanisms for maintaining identity or authentication state. A token can also be stored inside a cookie.

## What is CORS, and why do we need it?

CORS (Cross-Origin Resource Sharing) is a browser security mechanism that controls whether a web application running on one origin can access resources from another origin.

An origin consists of the protocol, domain, and port.

For example:

- Frontend: `https://frontend.com`
- Backend: `https://api.example.com`

Since these are different origins, the browser applies CORS rule

## What is JWT? Explain its structure and how JWT-based authentication works.

JWT (JSON Web Token) is a compact, URL-safe token format used to securely transmit claims between parties. It is commonly used for authentication and authorization.

A JWT consists of three parts:

1. Header – Contains token type and signing algorithm.
2. Payload – Contains claims such as user ID, role, and expiration.
3. Signature – Used to verify token integrity and authenticity.

Structure:

```
Header.Payload.Signature
```

Example payload:

```
{
  "userId": 101,
  "role": "admin",
  "exp": 1790000000
}
```

How JWT authentication works:

1. User submits login credentials.
2. Server validates credentials.
3. Server generates and signs a JWT.
4. Client stores the token securely.
5. Client sends the token with subsequent requests.
6. Server validates the signature and relevant claims.
7. If valid, the request is processed.

Example:

```
GET /api/profile
Authorization: Bearer <JWT_TOKEN>
```

Important interview points:

- JWT payload is Base64URL encoded, not encrypted by default.
- Never store sensitive information in an ordinary JWT payload.
- Tokens should have expiration times.
- HTTPS should always be used.
- JWT signatures protect integrity, not confidentiality.
