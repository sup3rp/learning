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
   <li><b>Consistency is key - </b> </li>
   <li><b>KISS - </b> </li>
   <li><b>Make use of HTTP Status Codes - </b> </li>
   <li><b>Return JSON, not plain text! - </b> </li>
   <li><b>Handle errors - </b> </li>
   <li><b>Security - </b> </li>
   <li><b>Incorporate pagination - </b> </li>
   <li><b>Versioning - </b> </li>
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

