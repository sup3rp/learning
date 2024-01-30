TODO: Sum up the best practices for API design 
Some sources: 

&utm_content=g-p-c&d=7013y000002O1f0AAC&nc=7013y000002O1WqAAK&gad_source=1&gclid=Cj0KCQiAwbitBhDIARIsABfFYIJPUdi-T95fA-aEZdwqPQPMkKmJT9C1TiYSvgqGyOMJxZc_0fLuL1UaAjuWEALw_wcB&gclsrc=aw.ds


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h3 align="center">🏭 API Best Practices. 🏭</h3>
  <p>Sources: </p>
  <p>https://medium.com/@techworldwithmilan/rest-api-design-best-practices-2eb5e749d428 </p>
  <p>https://blog.dreamfactory.com/best-practices-for-naming-rest-api-endpoints/</p>
  <p>https://www.mulesoft.com/sem/lp/whitepaper/api/design-apis?&utm_source=google&utm_medium=cpc&utm_campaign=fy24-g-mash-south-search-api-design&utm_term=api%20design%20best%20practices </p>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#what-is-an-api?">What is an API?</a></li>
    <li><a href="#different-types-of-apis">Different types of APIs</a></li>
    <li><a href="#different-types-of-web-apis">Different types of Web APIs</a></li>
    <li><a href="#rest">REST</a></li>
    <li><a href="#rpc">RPC</a></li>
    <li><a href="#soap">SOAP</a></li>
    <li><a href="#websocket">WebSocket</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ol>
</details>

<!-- What is an API? -->
## What is an API?
<p align="center">API stands for Application Programming Interface. It is a set of engineering standards, rules and tools that allows different software applications to be buil to communicate with each other. APIs define the methods and data formats that applications can use to request and exchange information. They provide a way for developers to access the functionality of a software component or service without having to understand its internal workings.</p>
<p>As a webdeveloper I'll focus more on APIs designed for web apps, since that is the main type I work with. Let's us focus on creating a guideline that we can follow whenever we need to create an API.</p>

<!-- Different types of APIs -->
## Different types of APIs

APIs can be categorized into different types, including:
<ol>
    <li><b>Web APIs (or HTTP APIs):</b> These APIs enable communication over the web using standard protocols such as HTTP. REST (Representational State Transfer) and GraphQL are common styles of web APIs.</li>
    <li><b>Library APIs:</b> These APIs provide a set of functions or procedures that can be called by a program, allowing developers to use pre-built functionality without having to write the code from scratch.</li>
    <li><b>Operating System APIs: </b>These APIs provide a way for software applications to interact with the underlying operating system, accessing resources such as files, memory, and hardware devices.</li>
  </ol>

<!-- Different types of Web APIs -->
## Different types of Web APIs
There are various types of web APIs, each with its own characteristics and use cases. The main types of web APIs are RESTful APIs, RPC, SOAP, WebSocket and GraphQL APIs.

<!-- REST -->
## REST

### What is REST?
<p>RESTful APIs (Representational State Transfer) - The most used type of Web API, uses HTTP and it allows web apps to communicate in a client - server approach, where the server provides the client with the API. This type of API was first intented to be stateless, meaning the server does not save the state of the client, and also is very open to interpretation, which allows a great level of freedom but also a lot of opportunities to design an inconsistent/bad API.</p>
<p>Analysis:</p>
<ol>
   <li><b> Architecture Style - </b> REST is an architectural style that follows a set of constraints and principles, such as statelessness and uniform interface.</li>
   <li><b> Communication - </b> RESTful APIs use standard HTTP methods (GET, POST, PUT, DELETE) for communication. Each resource is identified by a unique URL.</li>
   <li><b> Data Format - </b> Commonly use JSON as the data format, but XML is also supported.</li>
   <li><b> Statelessness - </b> Each request from a client to a server must contain all the information needed to understand and fulfill the request. The server does not store the client's state between requests.</li>
</ol>
<p>Standards/Best practices:</p>
<ol>
   <li><b>Use nouns, not verbs - </b> Verbs should not be used in endpoint paths. Instead, the pathname should contain the nouns that identify the object to which the endpoint we are accessing or altering belongs. For example, instead of using <i>/getAllClients</i> to fetch all clients, use  <i>/clients</i>.</li>
   <li><b>Use plural resource nouns - </b>Use the plural form for resource nouns because this fits all types of endpoints. For example, instead of using <i>/employee/:id/</i>, use <i>/employees/:id/</i>.</li>
   <li><b>Consistency is key - </b> Created a robust, predictable and consistent API that clients can use. This will allow client side development to be more quick and less error prune.</li>
   <li><b>Resource oriented - </b>Endpoints should be resource-oriented. For example, if you want to design an API for users: <i>/users</i> will return all users, <i>/users/124</i> will return the resource 124 from users</li>, <i>/users/124?page=1&page_size=10</i> will return the resource 124 from users with pagination, requesting page 1 with an offset of 10.
   <li><b>Make use of HTTP Status Codes - </b> This is one is really important. We should always return HTTP status codes as this is an industry standard. This is even more important if we are designing an API to be used by clients that we don't develop. The status codes should be used for the same outcomes across the API:
    <ol>
      <li>200 for general success.</li>
      <li>201 for successful creation.</li>
      <li>202 for a successful request.</li>
      <li>204 for no content.</li>
      <li>307 for redirected content.</li>
      <li>400 for bad requests.</li>
      <li>401 for unauthorized requests.</li>
      <li>403 for missing permissions.</li>
      <li>404 for lacking resources.</li>
      <li>500 for internal errors.</li>
      <li>501 for not implemented.</li>
      <li>502 for bad gateway.</li>
      <li>503 for service unavailable.</li>
      <li>504 for gateway timeout.</li>
    </ol>
   </li>
   <li><b>Return JSON, not plain text! - </b> REST APIs should accept and return JSON as this is the standard in the industry. JSON is a type of data structure that will aid clients and servers processing requests.</li>
   <li><b>Handle errors - </b> Return codes between 400 and 5xx and return details in the response body along with the status code.</li>
   <li><b>Security - </b> Use SSL/TLS, API keys.</li>
   <li><b>Incorporate pagination - </b> Design for the future, included pagination whenever you need to return a lot of resources. Use <i>page</i> and <i>page_size</i> as arguments.</li>
   <li><b>Versioning - </b> Design for the future, predicting that the API must be retrocompatible sometime in the future, design from day 1 an API that can allow versioning. For example <i>api/v1/products/124</i>.</li>
   <li><b>Documentation - </b> Use proper standards like OpenAPI definition, use tools as Swagger, Postman and Stoplight.</li>
</ol>

### The X social network API case study 


<!-- RPC -->
## RPC

<!-- SOAP -->
## SOAP

<!-- WebSocket -->
## WebSocket

<!-- GraphQL -->
## GraphQL

