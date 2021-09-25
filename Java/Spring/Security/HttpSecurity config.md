# HttpSecurity config

## Request matcher

By default the Http Security will be applied to all requests. By specify request matcher, Http security will be restricted to specific requests.

## Login

### `oauth2Login()`

This will add `OAuth2LoginConfigurer`, which will add:

* `OAuth2AuthorizationRequestRedirectFilter` for handling request from `"/oauth2/authorization/{registrationId}"`(default) by creating request to the authenticate service. The request is created using `OAuth2AuthorizationRequestResolver`.
* `OAuth2LoginAuthenticationFilter` for handle redirect request after sucessfuly login by authenticate service, in `"/login/oauth2/code/{...}"` (default).

### `formLogin()`

### `saml2Login()`

## Logout

Configuring `logout()` will add a `LogoutFilter`. This will handle logout request at `"/logout"` (configurable). The accepted method is POST if crpf is disabled, otherwise all common methods is accepted.  
After the user logout, we could configured to either redirect to a url or use a logout handler by `logoutSuccessHandler(LogoutSuccessHandler)`

## Add filter

Spring security defined a list of filters, whose order is 100 from each other. The lower order filter will be executed first.

Add filter can add the filter before, after or at that predefined filter (if no filter registered yet) with `atFilterBefore(Filter, Class<? extends Filter>)`,  `atFilterAfter(Filter, Class<? extends Filter>)` and `atFilter(Filter)`

## Authorize requests

Allow to restrict requests base on request matcher. They can require to has a role, authenticated, not required, etc.  
The matchers is consider in order, so if a formal matcher is matched, the latter won't be executed.

```java
http.authorizeRequests()
    .antMatchers("/public").permitAll()
    .antMatchers("/admin/**").hasRole("ADMIN")
    .anyRequest().hasRole("USER").authenticated()
```
