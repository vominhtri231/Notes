# Request matcher

`RequestMatcher` is used to match `HttpServletRequest`.

Some type of `RequestMatcher`:

1. `AntPathRequestMatcher`: match by ant-style
  
  Some general rule:

  * `?` : matches one character
  * `*` : matches one or more character
  * `**` : matches one or more directory

2. `RegexRequestMatcher`: match by regex-style pattern
