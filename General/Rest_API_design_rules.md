# REST API design rules

## Method - action mapping

| Resource | Post           | Get           | Put         | Path               | Delete          |
| -------- | -------------- | ------------- | ----------- | ------------------ | --------------- |
| /dogs    | Create new dog | List all dogs | Bulk update |                    | Delete all dogs |
| /dogs/23 |                | Show A        | Updating A  | Partially update A | Delete A        |

**If the action don't fit into methods, consider**:

* Treat it like a resource, like what Github does with star action [link](https://docs.github.com/en/rest/reference/gists#star-a-gist)
* Restructure the action to appear like a field of resource. Eg: `activate` action could be mapped to `active` field and update via a PATH
* For some cases, where there are no sensible way to map the action. Eg: Search for multiple resource should using the endpoint `/search` even though it is not a resource

**PUT vs POST**

In practice, they can both use to update and create resources and we do not need to support both PUT and POST.

PUT method is defined to be idempotent, meaning that if we execute a POST method multiple times, all the executions should have no additional effects.  
=> You can update or create a new resource with the same url `PUT /resourceNames/<id>`. 
This also means you must know the resource before PUT calls.

For POST, we must use `POST /resourceNames` for creating a resource and `POST /resourceNames/<id>` for updating.

## Relation of resource

If a relation can only exist within the resource:

* GET tickets/12/messages : get all message of ticket 12
* POST tickets/12/messages : create message of ticket 12
* GET tickets/12/messages/5 : get message id 5 of ticket 12
* PUT tickets/12/messages/5 : get update message id 5 of ticket 12
  , etc

If a relation can exist independently form the resource, consider returning their id within the resource. The consumer will later call relation endpoint.

If a relation is generally requested along with the resource, consider offering functionality to embed the relation's representation

Eg: GET `/tickets/12?embed=customer.name,assigned_user`

This will get the customer name and assigned user along with the ticket

```json
{
  "id" : 12,
  "subject" : "I have a question!",
  "summary" : "Hi, ....",
  "customer" : {
    "name" : "Bob"
  },
  assigned_user: {
   "id" : 42,
   "name" : "Jim",
  }
}
```

## Endpoint rules

* Resource name is noun and plural - not having to deal with all plural and consistent api make consuming the API easier.
* Versioning is obligated, start with 'v' and end with a positive integer ( v1,v2,v2.4 etc ), in front of the resource ( /v1/dogs/123). This helps the API transition smoother as you can continue to support the old API version.

## Result filtering, sorting, searching and limiting fields

To keep the base resource API lean, filtering, sorting and searching should put as query parameters

* Filtering: Use unique field parameter for each field that implement filtering
  Eg: `GET /tickets?state=open` - retrieving open ticket

* Sorting: Allow sort parameter to take in list of fields, with negative unary to imply descending order
  Eg: `GET /tickets?sort=-priority,created_at` - retrieving ticket, sort by priority descending and then by created date

* Searching: When you need a full text search for a specific type of resource
  Eg: `GET /tickets?q=abc` - retrieving tickets that mention the word `abc`

* API consumer doesn't always need the full representation of the resource, the ability to select fields would minimize network traffic.
  Eg: `GET /ticket?field=id,subject`

* To make the API more pleasant to use, you could create alias for common queries.
  Eg: `GET /tickets/recently_closed` for getting recently closed tickets.

## HATEOAS - Hypermedia as the Engine of Application State

The constrain of REST design that include links for next possible actions inside output representation.

Even though RESTful design principle encourage us to apply HATEOAS, it have several down sides: the decision of using the link usually happens at coding time, not run time; the client have to store more data than it have to and increase cost for the network payload, etc.

## Envelope

Many APIs wrap response inside an envelop like this for including metadata, pagination info etc or support JSONP

```json
{
  "data" : {
    "id" : 123,
    "name" : "John"
  }
}
```

However, the new standards that are adopted like CORS or Link header making this technic becomes unnecessary.

If the envelope really needed for JSONP or if the client is incapable of working with the header, consider using a flag like `?envelope=true` and returning the wrapped response.

For pagination info, the new standard is using the Link header, like with the github API. You could add more customized header for that.

```json
Link: <https://api.github.com/user/repos?page=3&per_page=100>; rel="next", <https://api.github.com/user/repos?page=50&per_page=100>; rel="last"
Pagination-Count: 100
Pagination-Page: 5
Pagination-Limit: 20
```

## File Uploader

Common rule: avoid using BASE64 encode binary content in JSON request as possible. Instead, using:

1. Direct file upload  
   Using Content-Type for setting proper content.

```http
PUT /profile/1234/image HTTP/1.1
Content-Type: image/jpeg
Content-Length: 284

raw image content
```

2. Multipart Http request  
   If the request support multiple files or associate data

```http
POST /profile/1234/images HTTP/1.1
Content-Type: multipart/form-data; boundary=MultipartBoundry
Accept-Encoding: gzip, deflate

--MultipartBoundry
Content-Disposition: form-data; name="image"; filename="12348024_1150631324960893_344096225642532672_n.jpg"
Content-Type: image/jpeg

raw image content
--MultipartBoundry
Content-Disposition: form-data; name="category"

my-category
--MultipartBoundry
```

3. 2 step metadata - upload   
   First, a request for metadata is called, return a link for uploading => prevent single transaction wrapper

## Rate limiting

To prevent abuse, it a standard practice to limit rate of API call.  
The standard HTTP code for this is 429 - too many requests. The HTTP header should also inform the client with these standard headers:

* X-Rate-Limit-Limit - The number of allowed requests in the current period
* X-Rate-Limit-Remaining - The number of remaining requests in the current period
* X-Rate-Limit-Reset - The number of seconds left in the current period

## Authentication

Always using SSL to protect the API from hijacking  
A RESTful API should be stateless, should not depend on any cookies or sessions, but using access token.  
If the REST have to support JSONP, consider using `access_token` query parameter.

## Errors

A error body should contain an unique code that can be looked up in the docs, a useful message and possibly a description.

```json
{
  "code" : 1024,
  "message" : "Validation Failed",
  "errors" : [
    {
      "code" : 5432,
      "field" : "first_name",
      "message" : "First name cannot have fancy characters"
    },
    {
       "code" : 5622,
       "field" : "password",
       "message" : "Password cannot be blank"
    }
  ]
}
```

## Return codes

Reusing standard HTTP code if possible:

-- success

* 200 : ok

* 201 : created - response to a POST that results in a creation, should be combined with a Location header

* 204 : no content - successful request that won't return anything in the body

* 302 : attempt to redirect the page

* 304 : not modified - use cached data

-- client issues

* 400 : bad request - the request itself is invalid
* 401 : unauthorized - the request require user authorization
* 403 : forbidden - the authentication is not sufficient
* 404 : not found - can not found resource URI
* 422 : un-processable entity - cannot process entity (Eg image's format not right, missing fields, etc) - used in validate errors
* 429 : too many request - the call reaching the rate limit

-- server issues

* 500 : internal server error
* 502 : bad gateway - the server is acting as a proxy and get bad response from the other server
