HTTP (Hypertext Transfer Protocol) defines several request methods (also known as HTTP verbs) that indicate the desired action to be performed on a resource. Here are the commonly used HTTP request methods:

**GET**:
>The GET method is used to retrieve a representation of a resource identified by the given URI.
  It should not have any side effects on the server and can be repeated without changing the server's state. GET requests should only retrieve data and not modify it.

**POST:**
>The POST method is used to submit data to be processed by the identified resource. It is often used to create new resources on the server. Unlike GET, POST requests are not idempotent as each request can result in a different action or resource creation.

**PUT:**
>The PUT method is used to update an existing resource identified by the given URI. It replaces the entire representation of the resource with the new data provided in the request payload. PUT requests are idempotent, meaning multiple identical requests should have the same effect as a single request.

**PATCH:**
>The PATCH method is similar to PUT, but it is used to partially update an existing resource. The request payload contains only the changes to be applied to the resource, rather than replacing the entire representation. Like PUT, PATCH requests are idempotent.

**DELETE:**
>The DELETE method is used to remove a resource identified by the given URI. It deletes the specified resource from the server. DELETE requests are idempotent, meaning multiple identical requests should have the same effect as a single request.

**HEAD:**
>The HEAD method is similar to GET, but it retrieves only the headers of the response without the actual response body. It is often used to check the status or metadata of a resource without fetching the entire content.

**OPTIONS:**
>The OPTIONS method is used to retrieve the communication options available for a given resource or server. It allows the client to determine the supported methods, headers, and other capabilities of the server.

**CONNECT:**
>The CONNECT method is primarily used by web proxies to establish a tunnel connection to the destination server. It is typically used in HTTP tunneling or SSL/TLS tunneling scenarios. The CONNECT request instructs the proxy to set up a connection to the requested host and port, allowing the client to communicate directly with the target server.

**TRACE:**
>The TRACE method is used to retrieve the loopback message of an HTTP request. It is primarily used for diagnostic or debugging purposes. When a server receives a TRACE request, it should return the entire request back to the client in the response body. TRACE can be helpful in understanding how intermediaries modify or handle requests.

