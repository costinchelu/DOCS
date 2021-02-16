## What is REST

REST stands for **Representational State Transfer**.

It means when a RESTful API is called, the <u>server will transfer to the client a representation of the state of the requested resource</u>.

For example, when a developer calls Instagram API to fetch a specific user (the resource), the API will return the state of that user, including their name, the number of posts that user posted on Instagram so far, how many followers they have, and more.

The representation of the state can be in a JSON format, and probably for most APIs this is indeed the case. It can also be in XML or HTML format.

What the server does when you, the client, call one of its APIs depends on 2 things that you need to provide to the server:
- An identifier for the resource you are interested in. This is the URL for the resource, also known as the <u>endpoint</u>. In fact, URL stands for Uniform Resource Locator.
- The operation you want the server to perform on that resource, in the form of an HTTP method, or verb. <u>The common HTTP methods are GET, POST, PUT, and DELETE.</u>

For example, fetching a specific Twitter user, using Twitter’s RESTful API, will require a URL that identify that user and the HTTP method GET.

In order for an API to be RESTful, it has to adhere to 6 constraints:
- Uniform interface
- Client — server separation
- Stateless
- Layered system
- Cacheable
- Code-on-demand (optional)

**Stateless** means the server does not remember anything about the user who uses the API. It doesn’t remember if the user of the API already sent a GET request for the same resource in the past, it doesn’t remember which resources the user of the API requested before, and so on.  
Each individual request contains all the information the server needs to perform the request and return a response, regardless of other requests made by the same API user.  
If the data is **cacheable**, it might contain some sort of a version number. The version number is what makes caching possible: since the client knows which version of the data it already has (from a previous response), the client can avoid requesting the same data again and again. The client should also know if the current version of the data is expired, in which case the client will know it should send another request to the server to get the most updated data about the state of a resource.

## What is Resource

REST architecture treats every content as a resource. These resources can be Text Files, Html Pages, Images, Videos or Dynamic Business Data. REST Server simply provides access to resources and REST client accesses and modifies the resources. Here each resource is identified by URIs/ Global IDs. REST uses various representations to represent a resource where Text, JSON, XML (most popular representations of resources are XML and JSON).  
A resource in REST is a similar object in object oriented programming or is like an entity in a database. Once a resource is identified then its representation is to be decided using a standard format so that the server can send the resource in the above said format and client can understand the same format.

## Which kind of requests are mapped to  which methods

| HTTP Verb | CRUD           | Entire Collection (e.g. /customers)      | Specific Item (e.g. /customers/{id})     |
|-----------|----------------|------------------------------------------|------------------------------------------|
| POST      | Create         | 201 (Created), 'Location' header with link to /customers/{id} containing new ID. | 404 (Not Found), 409 (Conflict) if resource already exists.. |
| GET       | Read           | 200 (OK), list of customers. Use pagination, sorting and filtering to navigate big lists. | 200 (OK), single customer. 404 (Not Found), if ID not found or invalid. |
| PUT       | Update/Replace | 405 (Method Not Allowed), unless you want to update/replace every resource in the entire collection. | 200 (OK) or 204 (No Content). 404 (Not Found), if ID not found or invalid. |
| PATCH     | Update/Modify  | 405 (Method Not Allowed), unless you want to modify the collection itself. | 200 (OK) or 204 (No Content). 404 (Not Found), if ID not found or invalid. |
| DELETE    | Delete         | 405 (Method Not Allowed), unless you want to delete the whole collection—not often desirable. | 200 (OK). 404 (Not Found), if ID not found or invalid. |

The **POST** verb is most-often utilized to **create** new resources. In particular, it's used to create subordinate resources. That is, subordinate to some other (e.g. parent) resource. In other words, when creating a new resource, POST to the parent and the service takes care of associating the new resource with the parent, assigning an ID (new resource URI), etc.

On successful creation, return HTTP status 201, returning a Location header with a link to the newly-created resource with the 201 HTTP status.

POST is neither safe nor idempotent. It is therefore recommended for non-idempotent resource requests. Making two identical POST requests will most-likely result in two resources containing the same information.

The HTTP **GET** method is used to **read** (or retrieve) a representation of a resource. In the “happy” (or non-error) path, GET returns a representation in XML or JSON and an HTTP response code of 200 (OK). In an error case, it most often returns a 404 (NOT FOUND) or 400 (BAD REQUEST).

According to the design of the HTTP specification, GET (along with HEAD) requests are used only to read data and not change it. Therefore, when used this way, they are considered safe. That is, they can be called without risk of data modification or corruption—calling it once has the same effect as calling it 10 times, or none at all. Additionally, GET (and HEAD) is idempotent, which means that making multiple identical requests ends up having the same result as a single request.

Do not expose unsafe operations via GET—it should never modify any resources on the server.

**PUT** is most-often utilized for **update** capabilities, PUT-ing to a known resource URI with the request body containing the newly-updated representation of the original resource.

However, PUT can also be used to create a resource in the case where the resource ID is chosen by the client instead of by the server. In other words, if the PUT is to a URI that contains the value of a non-existent resource ID. Again, the request body contains a resource representation. Many feel this is convoluted and confusing. Consequently, this method of creation should be used sparingly, if at all.

Alternatively, use POST to create new resources and provide the client-defined ID in the body representation—presumably to a URI that doesn't include the ID of the resource (see POST below).

On successful update, return 200 (or 204 if not returning any content in the body) from a PUT. If using PUT for create, return HTTP status 201 on successful creation. A body in the response is optional—providing one consumes more bandwidth. It is not necessary to return a link via a Location header in the creation case since the client already set the resource ID.

PUT is not a safe operation, in that it modifies (or creates) state on the server, but it is idempotent. In other words, if you create or update a resource using PUT and then make that same call again, the resource is still there and still has the same state as it did with the first call.

If, for instance, calling PUT on a resource increments a counter within the resource, the call is no longer idempotent. Sometimes that happens and it may be enough to document that the call is not idempotent. However, it's recommended to keep PUT requests idempotent. It is strongly recommended to use POST for non-idempotent requests.

**PATCH** is used for **modify** capabilities. The PATCH request only needs to contain the changes to the resource, not the complete resource.

This resembles PUT, but the body contains a set of instructions describing how a resource currently residing on the server should be modified to produce a new version. This means that the PATCH body should not just be a modified part of the resource, but in some kind of patch language like JSON Patch or XML Patch.

PATCH is neither safe nor idempotent. However, a PATCH request can be issued in such a way as to be idempotent, which also helps prevent bad outcomes from collisions between two PATCH requests on the same resource in a similar time frame. Collisions from multiple PATCH requests may be more dangerous than PUT collisions because some patch formats need to operate from a known base-point or else they will corrupt the resource. Clients using this kind of patch application should use a conditional request such that the request will fail if the resource has been updated since the client last accessed the resource. For example, the client can use a strong ETag in an If-Match header on the PATCH request.

**DELETE** is pretty easy to understand. It is used to **delete** a resource identified by a URI.

On successful deletion, return HTTP status 200 (OK) along with a response body, perhaps the representation of the deleted item (often demands too much bandwidth), or a wrapped response (see Return Values below). Either that or return HTTP status 204 (NO CONTENT) with no response body. In other words, a 204 status with no body, or the JSEND-style response and HTTP status 200 are the recommended responses.

HTTP-spec-wise, DELETE operations are idempotent. If you DELETE a resource, it's removed. Repeatedly calling DELETE on that resource ends up the same: the resource is gone. If calling DELETE say, decrements a counter (within the resource), the DELETE call is no longer idempotent. As mentioned previously, usage statistics and measurements may be updated while still considering the service idempotent as long as no resource data is changed. Using POST for non-idempotent resource requests is recommended.

There is a caveat about DELETE idempotence, however. Calling DELETE on a resource a second time will often return a 404 (NOT FOUND) since it was already removed and therefore is no longer findable. This, by some opinions, makes DELETE operations no longer idempotent, however, the end-state of the resource is the same. Returning a 404 is acceptable and communicates accurately the status of the call.


## HTTP status code classes

HTTP status codes are generally divided into five different classes. The first digit of the three-digit code shows which class it belongs to. 

- **Class 1xx – Informational**: If an HTTP status code 1xx is transmitted, the server informs the client that the request is in motion. This class combines codes that are responsible for delivering information to the client during the request.
- **Class 2xx – Success**: A 2xx code announces a successful operation. If this code is transmitted, it means that the client’s request was received by the server, understood, and accepted. 2xx codes are often sent at the same time as the desired website information, and the user often only takes notice of the website they have requested.
- **Class 3xx – Redirection**: A 3xx code shows that the server’s request was received. In order to ensure the request is successfully processed, further steps are needed from the client’send. 3xx codes appear during redirections and forwardings.
- **Class 4xx – Client error**: If a 4xx code appears then there’s been a client error. The server has received the request, but cannot perform it. The reason behind this is usually an incorrect request. Internet users will be made aware of this error by receiving an automatically generated HTML page.
- **Class 5xx – Server error**: A 5xx code is shown when the server has failed to perform the request. These server error codes report that the request cannot be performed at present or is not possible at all, which then leads to an HTML error page.      


## Most Important HTTP Status Codes

- **Status code 200 – OK**: The HTTP status code 200 shows that the request was successfully carried out. All the requested data was located on the web server and transferred to the client. Internet users do not usually see this code.
- **Status code 301 – Moved Permanently**: The 301 code means that the data requested from the client cannot be found under the given address since it has been moved permanently. Since the current location of the requested content is delivered in the status report, the browser can request the new address straightaway. The user is then forwarded to the new address and the old address is no longer valid. The 301 code also goes unnoticed because the URL in the address bar simply changes.
- **Status code 302 – Moved Temporarily**: Unlike the 301 code, which is a permanent redirection, the 302 informs the user that the requested data has temporarily been moved. With a 302 code the remaining information is specified so that an automatic redirection can take place. The old address remains valid.
- **Status code 400 – Bad Request**: The HTTP 400 code indicates that something went wrong with the client request: incorrect URL, incorrect cookies, outdated DNS records, files to large to upload, header too long.
- **Status code 403 – Forbidden**: The HTTP status code 403 tells the client that the requested data is access-protected and that the request cannot be performed due to the client not having authority. An automatically generated HTML page will let the user know about the access problem.
- **Status code 404 – Not Found**: If the server delivers a 404 message it means that the requested website information was not found on the server. It could be that the address no longer exists or the contents were moved to a new address without notice. Users that receive a 404 message should check whether the address was written correctly in the address bar. Any links to non-existing pages are known as ‘dead links’.
- **Status code 500 – Internal Server Error**: The 500 server response functions as a collection status code for unexpected server errors. If an error occurs on the server’s part, which prevents the requested data from being retrieved, this HTTP status code will automatically be issued. As well as sending an answer to the client the webserver also creates an internal error report. This should be analyzed by the website owner so that repairs can be carried out on the server software.
- **Status code 502 – Bad Gateway**: The 502 error is usually provided with the addition Bad Gateway or as a *“502 Bad Gateway Nginx”*, *“502 Bad Gateway Apache”*, or *“502 Bad Gateway registered endpoint failed to handle the request”* message. Next to the well-known 404 error (“Page not found”), the bad gateway error is one of the most common error messages received when surfing the internet. It’s delivered when the server, which is accessed via the main server, couldn’t forward the request. In this case, the first server functions only as a proxy or gateway. In principle, all queries on the internet are forwarded via gateways. That’s why this error message is often so frustrating: It’s generally not at all clear at which point in the process the request encounters the error.
- **Status code 503 ­– Service Unavailable**: If the user receives a 503 code it means that the relevant web server, which should deliver the requested information, is overloaded. The server response occasionally contains information about when the request can be processed at the earliest. Internet users can presume that an administrator is working on the problem and that the server will be available later on.
- **Status code 504 ­– Gateway Timeout**: The HTTP 504 response lets the client know that the cause of the failure was due to a timeout during the processing of a request. The sender of the message is the server in the communication chain that was unable to fulfil its function as a gateway, or proxy, as it didn’t receive a response from the next server (or service) within a specific time.