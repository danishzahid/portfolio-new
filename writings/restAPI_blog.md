---
title: "Understanding REST APIs: A Comprehensive Guide"
description: "A beginner-friendly blog exploring REST API concepts, offering a comprehensive understanding of APIs, particularly REST API, from scratch. Covers the topic from 0 to 1."
date: "2023-09-10"
---

# Understanding REST APIs: A Comprehensive Guide

## Introduction

**APIs:**
Imagine sitting in a restaurant. U dont directly go in the kitchen to order your food, instead u have a menu and you request for the food from it and the waiter delivers u the food after being processed/cooked in the kitchen. API works in the similar way. When u want to know the weather of some city from a weather app, u dont actually go there and fetch it or when u send a message to your friend sitting miles away over the whatsapp , it is the api which takes your request along with the message body , performs operation over the server and send it to your friend and u get the response , the blue tick/double tick that it is successfully delivered and red by your friend.
API stands for Application Programming Interface and it serve as a bridge a interface between different software applications, enabling them to communicate and interact with each other.
It define the methods and the format of the data that application can use to request and exchange information. APIs are very crucial in modern web application as it promotes modularity, interconnectivity, controlled data access of database, scalability and enhanced user experience.
We are using apis everyday , most of them are internally embedded in our application and we don't see what's happening under the hood.
To fetch the weather of a city, we just select the city in our weather app and it gives us the information like temperature , humidity and conditions. Have u ever wondered how is it doing so, where is the data stored and how are we able to get that so easily. Well under the hood , as soon as we select the city, it hits a URL with a get request(api method) with a request body that contains the coordinates of the city selected. Request goes to the server and after processing it comes with a response of success/failure and our application further process the response, extract the data like temperature and humidity and displays it on screen. Now u know how crucial it is. Let us deep dive into it.

## Types of APIs

Based on their use cases and functionality, there are several types of APIs, some of the common ones are listed below:

1. **REST APIs:** Follow REST principles. They use HTTP requests to perform CRUD(Create, Read, Update, Delete) operations and they are widely used for web services.

   _Example/Application:_ Consider a weather application. A REST API could provide weather data for a specific location when you enter the city name in the app. The app sends a GET request to the API server (e.g., GET /weather?city=NewYork), and the server responds with the weather information in a structured format like JSON or XML.

2. **SOAP API:** SOAP stands for SImple Object Access Protocol. They use XML for message format and can work over various protocols, including HTTP and SMTP for exchanging structured information in web services.

   _Example/Application:_ In an online banking system, a SOAP API can be used for fund transfer. When you initiate a fund transfer from your account to another, a SOAP request is sent to the bank's server containing details like account numbers, amounts, and authentication information.

3. **GraphQL APIs:** GraphQL APIs allow clients to request specific data from the server. Unlike REST APIs, where the server determines the response structure, in GraphQL, the client specifies the structure of the response which can help reduce over-fetching and under-fetching of data.

   _Example/Application:_ Imagine a social media platform. With a GraphQL API, a client (like a mobile app) can request specific fields from a user's profile, such as their name, profile picture, and recent posts. The client specifies the desired fields in the query, and the server responds with exactly that data, enhancing efficiency.

4. **Streaming APIs:** Allows for the continuous flow of data between the client and the server. They are commonly used for real time analytics, social media feeds, or live updates.

   _Example/Application:_ In a live sports scores application, a streaming API can be used to push real-time score updates to users' devices as the game progresses. Users receive instant notifications or updates without having to manually refresh the app, ensuring they get the latest information in real time.

5. **Webhooks:** Webhooks are the type of API that allows one system to send real time data to another system as soon as a specific event occurs. Web hooks are commonly used for event driven architecture and integrations.

   _Example/Application:_ In an e-commerce system, a webhook can be set up to notify the inventory management system whenever a product is sold. When a customer makes a purchase, the webhook sends a POST request to the inventory system, updating the stock quantity in real time without manual intervention.

## What is REST API?

Representational State Transfer, commonly known as REST, is an architectural style for designing networked applications. REST provides a set of constraints and principles for creating web services. In the context of web development, RESTful web services allow systems to communicate over the internet using the Hypertext Transfer Protocol (HTTP).

## Architectural Principles of REST

REST is based on several architectural principles that define how web services should be designed and interact with each other. These principles include:

1. **Statelessness:** RESTful interactions are stateless, meaning each request from a client to a server must contain all the information needed to understand and fulfill that request. The server does not store any client state between requests. Any session state is held on the client side.

2. **Client-Server Architecture:** REST separates the client and server into independent entities. The client is responsible for the user interface and user experience, while the server is responsible for processing requests, managing resources, and handling business logic. This separation enhances the scalability of the system.

3. **Uniform Interface:** RESTful systems have a uniform and consistent interface. This principle is further broken down into several constraints:

   - **Resource Identification:** Resources (data objects or services) are identified by URIs (Uniform Resource Identifiers). Each resource must have a unique URI that distinguishes it from other resources.
   - **Resource Manipulation through Representations:** Clients interact with resources by exchanging representations of the resource state. These representations can be in various formats such as JSON, XML, or HTML. The client can modify the resource by manipulating its representation.
   - **Self-Descriptive Messages:** Each message sent from the client to the server (or vice versa) must contain all the information needed to understand and process the request. This includes information about the resource being accessed and the desired action to be performed.
   - **Hypermedia as the Engine of Application State (HATEOAS):** In addition to the data, responses from the server contain hyperlinks that guide the client on possible actions it can take next. HATEOAS allows the client to navigate the application's capabilities dynamically.

4. **Stateless Communication:** Communication between the client and server should be stateless. Each request from the client to the server must contain all the necessary information, and the server's response must contain all the information the client needs.

5. **Layered System:** REST allows for the use of a layered architecture, where each component (or layer) has a specific functionality and interacts only with the adjacent layers. This separation enhances flexibility and scalability, as components can be modified or replaced without affecting the entire system.

By adhering to these architectural principles, RESTful APIs ensure a scalable, stateless, and uniform approach to web service development, making them widely used in modern web

# URIs and HTTP Methods in REST:

1. **Resources:**

In REST APIs, a resource is an object or service that can be accessed via a URI. Resources can be data objects, services, or entities, such as users, products, or documents. For example, in a social media application, users, posts, comments, and likes can all be considered resources. Resources are the key abstractions that REST APIs expose to clients.

2. **URIs (Uniform Resource Identifiers):**

URIs are unique addresses used to identify resources in the context of a RESTful API. A URI consists of the following components:

- **Scheme:** Specifies the protocol used, such as "http" or "https."
- **Host:** Indicates the domain name or IP address of the server.
- **Port:** Optional, specifies the port number to connect to on the server.
- **Path:** Specifies the specific resource or endpoint on the server.
- **Query Parameters:** Optional, used to send additional data to the server.
- **Fragment:** Optional, identifies a specific section within the resource, often used in web pages.

_Example URI:_ [https://api.example.com/users/123](https://api.example.com/users/123)

In this URI, https is the scheme, api.example.com is the host, and /users/123 is the path, identifying a specific user resource.

3. **HTTP Methods (GET, POST, PUT, DELETE):**

RESTful APIs use standard HTTP methods to perform actions on resources. Each HTTP method has a specific purpose:

- **GET:** Used to retrieve data from a specified resource. GET requests should only retrieve data and not modify it. For example, fetching information about a user or a list of products.
- **POST:** Used to submit data to be processed to a specified resource. POST requests are often used for creating new resources. For example, creating a new user or posting a comment.
- **PUT:** Used to update a specific resource with new data. PUT requests are idempotent, meaning making the same request multiple times produces the same result. For example, updating a user's profile information.
- **DELETE:** Used to remove a specific resource. DELETE requests delete the specified resource from the server. For example, deleting a user account or removing a post.

By using these HTTP methods with appropriate URIs, clients can perform various operations on resources within a RESTful API. The combination of resources, URIs, and HTTP methods forms the basis of the REST architectural style, enabling a scalable and stateless communication model between clients and servers.

# Concept of Stateless Communication in REST APIs:

Statelessness, in the context of REST APIs, means that each request from a client to a server must contain all the information needed to understand and fulfill that request. The server does not store any information about the client's state between requests. This statelessness simplifies the server, as it does not need to maintain session information, and each request can be treated independently.

In a stateless communication model:

1. **No Session Information:** The server does not store any session data about the client between requests. Each request is treated in isolation.
2. **Independence:** Each request from a client to a server contains all the necessary information for the server to understand and process the request. The server's response contains all the information needed by the client.
3. **Scalability:** Stateless communication enhances scalability since servers do not need to keep track of client states. It allows servers to handle a large number of concurrent requests from different clients efficiently.
4. **Simplicity:** Stateless APIs are simpler to design and maintain. There are no complexities related to managing session data, making the API implementation straightforward.

# Understanding the Role of HTTP Status Codes in REST API Responses:

HTTP status codes are a crucial part of RESTful API responses. They provide information about the status of a request made by a client to a server. These codes indicate whether a specific HTTP request has been successfully completed, if it needs further action, or if an error occurred during the process. Understanding these status codes is essential for both the client and server to comprehend the outcome of an API request. Here are some of the common HTTP status codes used in REST API responses and their meanings:

## 1. 2xx Series (Success):

- **200 OK:** The request was successful, and the server has returned the requested data.
- **201 Created:** The request was successful, and a new resource was created as a result of the request.
- **204 No Content:** The request was successful, but there is no data to return (often used for DELETE operations).

## 2. 3xx Series (Redirection):

- **301 Moved Permanently:** The requested resource has been permanently moved to a new location. Clients should update their bookmarks or links.
- **302 Found:** The requested resource has been temporarily moved to a different URI. The client should continue to use the original URI.
- **304 Not Modified:** The client's cached version of the resource is still valid, and the server doesn't need to send a new copy.

## 3. 4xx Series (Client Errors):

- **400 Bad Request:** The server could not understand the request due to invalid syntax or missing parameters.
- **401 Unauthorized:** The client must authenticate itself to get the requested response.
- **403 Forbidden:** The client does not have the necessary permissions to access the requested resource.
- **404 Not Found:** The requested resource could not be found on the server.
- **422 Unprocessable Entity:** The server understands the request, but it cannot process the provided data (often used in validation failures).

## 4. 5xx Series (Server Errors):

- **500 Internal Server Error:** A generic error message indicating a problem on the server. The client request is valid, but the server encountered an unexpected condition.
- **503 Service Unavailable:** The server is currently unable to handle the request due to temporary overloading or maintenance of the server.

HTTP status codes in REST API responses are important for clear communication, error handling, debugging, and designing APIs.

# REST vs Non-REST APIs

Traditional APIs, often referred to as non-REST APIs, encompass various API styles that existed before the widespread adoption of REST (Representational State Transfer) architectural principles. These APIs are designed using different protocols, data formats, and communication patterns. Here are some key characteristics and explanations of traditional/non-REST APIs:

## Characteristics of Traditional/Non-REST APIs:

- **Protocol Variety:** Non-REST APIs use different protocols for communication, such as SOAP (Simple Object Access Protocol), XML-RPC, CORBA (Common Object Request Broker Architecture), and RPC (Remote Procedure Call). Each protocol has its own rules and specifications for API communication.

- **Data Formats:** Traditional APIs often use XML (eXtensible Markup Language) or sometimes JSON (JavaScript Object Notation) for data exchange. XML was a popular choice due to its structured nature, allowing complex data to be transmitted.

- **Complex Operations:** Non-REST APIs may involve complex operations and can expose a wide range of functionalities. They often rely on custom methods or procedures defined by the API provider.

- **Stateful Communication:** Some non-REST APIs can be stateful, meaning they maintain information about the client's state between requests. Session management is handled by the server, requiring clients to establish and maintain sessions.

- **Service Description:** APIs using protocols like SOAP often come with detailed service descriptions provided in WSDL (Web Services Description Language) documents. WSDL documents define the operations, input/output parameters, and communication details of the API.

## Examples of Traditional/Non-REST APIs:

- **SOAP APIs:** SOAP (Simple Object Access Protocol) APIs use XML for message formatting and are protocol-agnostic, meaning they can work over various underlying protocols, such as HTTP, SMTP, or JMS (Java Message Service).

- **XML-RPC APIs:** XML-RPC is a remote procedure call (RPC) protocol encoded in XML. It allows programs running on different operating systems and environments to communicate using HTTP for transport and XML for encoding.

- **CORBA APIs:** CORBA (Common Object Request Broker Architecture) is a middleware technology that enables communication between objects located in a networked computing environment. CORBA APIs are complex and support multiple programming languages.

- **JSON-RPC APIs:** Similar to XML-RPC, JSON-RPC is a remote procedure call (RPC) protocol encoded in JSON. It provides a more lightweight alternative to XML-RPC for transmitting data between a client and a server.

## Comparison of REST APIs and SOAP APIs:

### 1. Protocol:

**REST APIs:**

- Protocol: Primarily use HTTP/HTTPS protocol.
- Flexibility: REST APIs are not bound to any specific protocol and can work with other protocols if needed. However, HTTP is the most common choice.
- Statelessness: REST APIs are stateless, meaning each request from a client to the server contains all the information needed to understand and fulfill the request.

**SOAP APIs:**

- Protocol: Use XML-based protocol, often over HTTP/HTTPS. Can also work with other protocols such as SMTP and JMS.
- Rigidity: SOAP APIs are rigidly defined and require adherence to the XML structure defined in the WSDL (Web Services Description Language) document.
- Statefulness: SOAP APIs can be stateful, meaning they can maintain session information between requests if needed.

### 2. Data Format:

**REST APIs:**

- Data Format: Typically use lightweight data formats like JSON (JavaScript Object Notation) or XML for data exchange. JSON is more commonly used due to its simplicity and ease of parsing in JavaScript and other programming languages.
- Human-Readable: JSON data is human-readable and easy to understand, making it popular for web APIs.

**SOAP APIs:**

- Data Format: Use XML (eXtensible Markup Language) for data exchange. XML is structured and allows for complex data schemas.
- Verbose: XML is more verbose than JSON, making SOAP messages larger and potentially slower to transmit over the network.

### 3. Usage:

**REST APIs:**

- Usage: REST APIs are widely used for public APIs, web services, and mobile applications.
- Simplicity: REST APIs are simple to use and understand, making them a popular choice for developers.

**SOAP APIs:**

- Usage: SOAP APIs are often used in enterprise-level applications, web services where security and transactional capabilities are critical, and scenarios where a strict contract between client and server is necessary.
- Complexity: SOAP APIs are more complex due to their rigid structure and the need to define operations in WSDL documents.

REST APIs offer significant advantages over non-RESTful APIs due to their simplicity, flexibility, and scalability. REST APIs use standard HTTP methods and data formats, making them easy to understand and work with. They are flexible, allowing communication over various protocols and supporting multiple data formats. Additionally, REST APIs are stateless, enabling them to handle a large number of requests efficiently, and they can scale horizontally by adding more servers to meet increased demand. These qualities make REST APIs a preferred choice for modern web services, ensuring straightforward development, adaptability, and efficient scalability.

## Key Components of REST APIs:

### Resource URI Design:

Designing meaningful and intuitive URIs for resources in a REST API is essential for creating a user-friendly and developer-friendly interface. Here's how to approach it:

1. **Use Nouns for Resources:** URIs should represent resources, so use nouns to name them. For example, if you have a resource for users, the URI could be /users.

2. **Be Consistent:** Maintain consistency in naming conventions throughout your API. Choose a format (e.g., singular or plural nouns) and stick with it for all resource URIs.

3. **Hierarchy for Complex Resources:** If your resources have relationships, represent them hierarchically in the URI. For instance, if a user has posts, the URI could be /users/{userID}/posts/{postID}.

4. **Avoid Verbs:** URIs should not include action verbs. Use HTTP methods (GET, POST, PUT, DELETE) to indicate actions. For example, instead of /getUserByID, use /users/{userID} and perform a GET request.

5. **Use Hyphens or Underscores:** Choose either hyphens or underscores to separate words in URIs, based on your preference. For example, /user-profiles or /user_profiles.

6. **Versioning:** If your API evolves, consider including the version number in the URI to ensure backward compatibility, like /v1/users.

7. **Keep URIs Intuitive:** Make URIs easy to guess and remember. Intuitive URIs enhance the usability of your API. Avoid cryptic codes or IDs in URIs whenever possible.

8. **Avoid Query Parameters for Resource Identification:** Use query parameters for filtering, sorting, or pagination, but not for identifying resources. Important resource identifiers should be in the URI path.

By following these principles, you create a clear, consistent, and user-friendly URI structure, making it easier for developers to understand and interact with your API.

## HTTP Methods:

HTTP methods, also known as HTTP verbs, are actions that can be performed on a resource identified by a URI (Uniform Resource Identifier) in the context of the HTTP protocol, which is the foundation of data communication on the internet. These methods define the operation that the client requests to be applied to the resource. Here's a brief explanation of common HTTP methods:

### GET:

- **Use Case:** GET method is used to request data from a specified resource. It retrieves information without modifying the resource. GET requests are safe and idempotent, meaning they don't change the state of the server and can be repeated without different outcomes.
- **Example:** Retrieving a user's profile (GET /users/{userID}) or fetching a list of products (GET /products).

### POST:

- **Use Case:** POST method is used to submit data to be processed to a specified resource. It is often used for creating new resources. POST requests are not idempotent, meaning making the same request multiple times may result in different outcomes.
- **Example:** Creating a new user (POST /users) or adding a comment to a post (POST /posts/{postID}/comments).

### PUT:

- **Use Case:** PUT method is used to update a specific resource with new data. It replaces the existing resource or creates it if it doesn't exist. PUT requests are idempotent, making the same request multiple times produce the same result.
- **Example:** Updating a user's profile information (PUT /users/{userID}) or modifying an existing article (PUT /articles/{articleID}).

### DELETE:

- **Use Case:** DELETE method is used to remove a specific resource. It deletes the resource identified by the URI. DELETE requests are idempotent, meaning calling the same request multiple times will have the same effect.
- **Example:** Deleting a user account (DELETE /users/{userID}) or removing a comment from a post (DELETE /posts/{postID}/comments/{commentID}).

In summary, GET is for retrieving data, POST is for creating new resources, PUT is for updating existing resources, and DELETE is for removing resources. These methods provide a standardized way for clients to interact with resources on the web, ensuring predictable and consistent behavior across different web services.

# Request and Response Formats in REST APIs

Request and Response Formats in REST APIs often use JSON (JavaScript Object Notation) and XML (eXtensible Markup Language) as common data exchange formats.

## JSON (JavaScript Object Notation):

- **Simplicity:** JSON is easy to read and write. Its syntax closely resembles JavaScript objects.
- **Data Structure:** Supports key-value pairs and arrays, providing a simple way to represent complex data structures.
- **Readability:** Human-readable format makes it popular for APIs and configurations.
- **Usage:** Widely used in modern REST APIs due to its simplicity and ease of parsing in various programming languages.

```json
{
  "user": {
    "id": 1,
    "name": "John Doe",
    "email": "johndoe@example.com",
    "roles": ["user", "admin"],
    "address": {
      "city": "New York",
      "zipcode": "10001"
    }
  }
}
```

## XML (eXtensible Markup Language):

- **Hierarchical Structure:** XML documents have a hierarchical structure, making it suitable for representing complex data relationships.
- **Flexibility:** Allows defining custom tags and attributes, providing flexibility in data representation.
- **Schema Validation:** Supports schema definition, allowing for strict validation of data structures.
- **Usage:** Commonly used in legacy systems and enterprise applications, although JSON has gained more popularity in modern web APIs due to its simplicity.

```xml
<user>
  <id>1</id>
  <name>John Doe</name>
  <email>johndoe@example.com</email>
  <roles>
    <role>user</role>
    <role>admin</role>
  </roles>
  <address>
    <city>New York</city>
    <zipcode>10001</zipcode>
  </address>
</user>
```

Both formats achieve the same goal of representing the user object, but they use different syntax and structures to do so. JSON is more concise and easier to read, while XML provides a hierarchical structure with explicit tags. The choice between them depends on the preferences of developers and the specific requirements of the application.

## REST APIs Best Practices:

### HATEOAS (Hypermedia as the Engine of Application State) Concept:

HATEOAS is a principle in RESTful APIs where responses contain hyperlinks guiding clients on possible actions. It makes APIs self-descriptive, enabling dynamic navigation.

### Pagination and Filtering:

- **Pagination:** Breaks large datasets into smaller chunks (pages) for improved performance. APIs use parameters like `page` and `pageSize` for pagination.
- **Filtering:** Allows specific data requests based on criteria. Query parameters like `filter` narrow down datasets by attributes like date or category.

### Versioning:

API versioning maintains backward compatibility:

- **URI Path:** Use `/v1/resource`.
- **Custom Headers:** Employ `Accept-Version: v1`.
- **Query Parameters:** Utilize `/resource?version=v1`.

### Security:

#### Authentication Methods:

- **Basic Auth:** Sends credentials (username and password) with each request. Simple but less secure.
- **OAuth:** Delegates user authentication to a third-party service, providing access tokens.
- **JWT (JSON Web Tokens):** Compact tokens containing user info, ensuring secure authentication.

#### Data Encryption:

- **SSL/TLS (HTTPS):** Encrypts data between client and server, ensuring confidentiality and integrity.

Each aspect is crucial for designing secure, efficient, and adaptable REST APIs, enhancing user and developer experiences.

## Conclusion:

In web development, REST APIs are foundational, offering a standardized, scalable, and versatile approach. From foundational principles to advanced techniques like HATEOAS, pagination, versioning, and security methods, REST APIs embody simplicity and adaptability. Mastering RESTful API development opens gates to innovation. Dive in, experiment, and leverage online resources as REST APIs continue shaping the digital landscape.

**I hope you’ve learned something good from here for sure. Thanks for the read.**
