# Open ID

## Origin

Since the OAuth is designed for authorization, using it for authentication is hard (no standard way to get user information) => OpenID is built on top of OAuth for authentication.  

To tell the authorization server that the request is OpenID, simply add scope `openid` to the request.

## Feature

The OpenId is built on top of OAuth and added:

* ID token  
  When user change the authentication code, they would get the ID token along with the access token.  
  The ID token's format is JWT.
* User info endpoint
* Standard set of scopes
