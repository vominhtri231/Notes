|Resource | Post | Get | Put | Delete|
|---|---|---|---|---|
|/dogs|Create new dog|List all dogs| Bulk update| Delete all dogs|
|/dogs/23|  | Show A | Updating existing A | Delete A|

### Remarks
* Resource name is noun and plural.
* Versioning is obligated, start with 'v' and end with a positive integer ( v1,v2, etc ), in front of the resource ( /v1/dogs/123 ) 
* Common result code
    * 200 : ok
    * 302: attemp to redirect the page
    * 304 : not modified - use cached data
    * 400 : bad request - the request itself is invalid
    * 401 : unauthorized - the request require user authorization
    * 403 : forbidden - the authentication is not sufficent
    * 404 : not found - can not found rerouce URI
    * 422 : unprocessable entity - cannot process entity (Eg image's format not right, missing fields, etc)
    * 500 : internal server error