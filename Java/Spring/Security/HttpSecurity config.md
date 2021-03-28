# Config login
### `oauth2Login()`
This will add `OAuth2LoginConfigurer`, which will add:
* `OAuth2AuthorizationRequestRedirectFilter` for handling request from `/oauth2/authorization/{registrationId}`(by default) by creating request to the authenticate service. The request is created using `OAuth2AuthorizationRequestResolver`.
* `OAuth2LoginAuthenticationFilter` for handle login request after sucessfuly login by authenticate service, in `/login/oauth2/code/{...}` (by default).
### `formLogin()`
### `saml2Login()`