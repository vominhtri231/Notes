The authorization code is the temporary code that the client will later use to get an access token.

When the user successfully authorizes the application in the authorizing server,
it will redirect back to the application with a temporary code. 
The application will later exchange the code along with client id to for the access token.
This is for reducing the risk of intercepting the authorization code.

The authorization URL is usually has a format such as:
```http request
https://authorization-server.com/oauth/authorize
?client_id=a17c21ed
&response_type=code
&state=5ca75bd30
&redirect_uri=https%3A%2F%2Fexample-app.com%2Fauth
&scope=photos
```
**Note:**
* response_type=code : indicate that you want authorization code as response
* redirect_uri: the URL you want the user to be redirected (match with the one registered with the service)
* state: when user is redirected back, it will be included.
This would allow user to persist data before authenticating and retrieve it later on.
  
Exchanging the authorization code for access token required a
POST request with parameters:
* grand-type: must be “authorization_code”
* code
* client authentication