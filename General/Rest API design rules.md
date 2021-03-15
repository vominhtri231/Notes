|Resource | Post | Get | Put | Delete|
|---|---|---|---|---|
|/dogs|Create new dog|List all dogs| Bulk update| Delete all dogs|
|/dogs/23|  | Show A | Updating existing A | Delete A|

### Remarks
* Resource name is noun and plural.
* Versioning is obligated, start with 'v' and end with a positive integer ( v1,v2, etc ), in front of the resource ( /v1/dogs/123 ) 
* Common result code
    1. 500 : internal server error
    2. 200 : ok
    3. 304 : not modified - use cached data
    4. 400 : bad request - the request itself is invalid
    5. 401 : unauthorized - the request require user authorization
    6. 403 : forbidden - the authentication is not sufficent
    7. 404 : not found - can not found rerouce URI
    8. 422 : unprocessable entity - cannot process entity (Eg image's format not right, missing fields, etc)