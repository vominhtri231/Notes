# Content-Security-policy (CSP)

It's a HTTP response header for restricting how resources are loaded in a web page.

SCP is designed to mitigate XSS or Click Jacking.

## Directives

Each directive in CSP header define types of resource. If there are multiple directives, they are separated by `;`. There are some well known directives:

* default-src: resource like JS, images, css, etc.
* script-src: JS
* style-src: Css
* font-src
* object-src: `<object>`, `<embed>` or `<applet>`
* form-action: `<form>`

## Source list

It is used to defined how the resource is allowed. Some of them are:

| Source value         | Description                                 |
| -------------------- | ------------------------------------------- |
| `*`                  | Allowed any URL                             |
| `'none'`             | Prevents loading resources                  |
| `'self'`             | Allows resources from the same origin       |
| `domain.example.com` | Allow resources from a specific domain      |
| `*.example.com`      | Allow resource from any sub domain          |
| `http://example.com` | Allow resource from a domain and over HTTPS |
