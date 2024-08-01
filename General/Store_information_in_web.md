# Store information in web

## Session

Session is saved on server side. When there are a request to server, server will create a file to hold session info => The data will be available to all pages of the side.

If there are multiple backend servers, session replication is needed.

When user close browser, server will keep the session for a predetermined time before deleting it.

## Cookie

Cookie is saved on client side. It is essentially for saving session id for communicate with server side's session.

### Usage

Cookie will be set if the response has the header `Set-Cookie`. You could also set the cookie via the script.

```js
document.cookie = "a=1; Max-Age=12000; Secure"
```

Every time browser send a request, cookie will be sent along (condition applied). You could also access the cookie via the script.

```js
document.cookie
> "a=1; b=2; c=3"
```

## First-party and third-party cookie

Cookies that match domain of the current side, i.e, what displayed in the browser's address bar are referred as first-party cookies. Cookies that don't match domain of the current side is called third-party cookies. This lead to various problems like CSRF, request overhead, track user activity across multiple sites, etc.

### Some cookie's attributes

* domain - the domain it belongs. Cookie is private to the domain.
* path - the path that it will be sent.
* secure - the cookie only be sent via https.
* httpOnly - the cookie can not be access via script.
* sameSite - how cookie will be sent on cross-side request (not fully supported). Possible values:
  * strict (only be sent as first-party cookie)
  * lax (only be sent as first-party cookie, but allows navigation)
  * none (can be sent as third-party cookie).  

IETF proposes that cookie without sameSite attribute should be treat as `lax`, cookie with `sameSite=none` must be specified as `secure`
