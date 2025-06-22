Spring Security is based on Servlet Filters.

![](https://github.com/spring-guides/top-spring-security-architecture/raw/master/images/security-filters.png)

Spring Security installed a single Filter whose type is FilterChainProxy in the chain. Its position defined
by `SecurityProperties.DEFAULT_FILTER_ORDER`. From the perspective of the container, it's a single filter, but, inside
it, there are additional filters.

![](https://github.com/spring-guides/top-spring-security-architecture/raw/master/images/security-filters-dispatch.png)

There are can be multiple filter chains managed in the `FilterChainProxy`. The Spring Security will dispatch a request
to the first chain that matches it. Only one chain ever handles a request, so their orders maters.

### Creating and customizing filter chains

The default fallback filter (the one that match /** request) has the predefined order of 
`org.springframework.boot.autoconfigure.security.SecurityProperties.BASIC_AUTH_ORDER`.
You could switch it on/off by setting `security.basic.enabled`.  
To declare your own filter chain, add a `Bean` of type `WebSecurityConfigurer`
or `WebSecurityConfigurerAdapter`. Note that the order need to be lower than the default fallback filter.  
Despite the fact that only one chain ever handles a request, you can have more
precise control of authorization by setting additional matcher in the `HttpSecurity` configuration.

```java
@Configuration
@Order(SecurityProperties.BASIC_AUTH_ORDER - 10)
public class ApplicationConfigurerAdapter extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.antMatcher("/match1/**")
                .authorizeRequests()
                .antMatchers("/match1/user").hasRole("USER")
                .antMatchers("/match1/spam").hasRole("SPAM")
                .anyRequest().isAuthenticated();
    }
}
```