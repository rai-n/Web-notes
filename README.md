# Web-notes

![Cors example](images\cors.png)

## What is CORS

Let’s say you have a web application running on http://myapp.com that wants to make a request to an API hosted on http://myapi.com. Since the web application and the API are on different domains, this is considered a cross-origin request.

Before the actual request is sent, the browser will automatically send a preflight request to the server at http://myapi.com. This preflight request is an HTTP OPTIONS request that includes headers such as Access-Control-Request-Method, Access-Control-Request-Headers, and Origin to indicate the method, headers, and origin of the actual request.

The server at http://myapi.com will then respond to the preflight request with headers such as Access-Control-Allow-Origin, Access-Control-Allow-Methods, and Access-Control-Allow-Headers to indicate whether the actual request is allowed. If the server allows the request, then the browser will proceed to send the actual request.

For example, let’s say the web application wants to send a POST request with a custom header X-Custom-Header to http://myapi.com/data. The preflight request would look like this:

```
OPTIONS /data HTTP/1.1
Host: myapi.com
Origin: http://myapp.com
Access-Control-Request-Method: POST
Access-Control-Request-Headers: X-Custom-Header
 ```

The server at http://myapi.com might respond with something like this:

```
HTTP/1.1 200 OK
Access-Control-Allow-Origin: http://myapp.com
Access-Control-Allow-Methods: POST
Access-Control-Allow-Headers: X-Custom-Header
 ```

This response indicates that the server allows the actual POST request from http://myapp.com with the custom header X-Custom-Header. The browser will then proceed to send the actual POST request.

## Why is this necessary?
CORS (Cross-Origin Resource Sharing) and preflight requests are mechanisms that allow servers to specify which origins are allowed to access their resources. This is done to protect the resources on the server (myapi.com in our example) from being accessed by unauthorized origins.

By default, web browsers follow the same-origin policy, which means that a web page can only access resources from the same origin as the page itself. This policy is in place to prevent malicious websites from accessing sensitive data on other websites.

However, there are many legitimate use cases where a web page needs to access resources from a different origin. CORS and preflight requests provide a way for servers to explicitly allow cross-origin requests from specific origins while still protecting their resources from unauthorized access.

In our example, the preflight request and CORS headers allow the server at myapi.com to specify that it allows requests from myapp.com while still preventing requests from other origins. This helps protect the resources on myapi.com from being accessed by unauthorized origins.

