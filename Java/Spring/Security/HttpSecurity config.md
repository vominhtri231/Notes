# Login
### `oauth2Login()`
This will add `OAuth2LoginConfigurer`, which will add:
* `OAuth2AuthorizationRequestRedirectFilter` for handling request from `"/oauth2/authorization/{registrationId}"`(by default) by creating request to the authenticate service. The request is created using `OAuth2AuthorizationRequestResolver`.
* `OAuth2LoginAuthenticationFilter` for handle login request after sucessfuly login by authenticate service, in `"/login/oauth2/code/{...}"` (by default).
### `formLogin()`
### `saml2Login()`

# Logout

Configuring `logout()` will add a `LogoutFilter`. This will handle logout request at `"/logout"` (configurable). The accepted method is POST if crpf is disabled, otherwise all common methods is accepted.  
After the user logout, we could configured to either redirect to a url or handle the request to a handler.