# Overview
### Web and Hypertext
### URL, HTTP and HTML
### REST

# Specifications
### Query String
* as URI Component
* `application/x-form-urlencoded` (key=value&...)
* Complex Structure (Array, Nested Object)
  * Spring & WAS: `SearchDTO`
  * Express.js: `req.query`, `querystring`, `qs`

### Payload Body
* Method Semantics
* `Content-Length: 0`
  * Spring & WAS: `@RequestBody SearchDTO`
  * Express.js: `req.body`, `body-parser`, `Content-Type`

# Security
### Cookie

### XSS
* Scenario

### CSRF
* Scenario
* Prevent Technics: `token`
* Safe Methods: GET(?)

### TLS

# Practices
assume environments with **Ajax**.\
See also [API Design Guide](https://cloud.google.com/apis/design/standard_fields).

| Method | Query | Body | Usecase | Note |
| - | :-: | :-: | - | - |
| GET | Used | ~~not Used~~ | Search, Minimized Response| |
| POST | ~~not Used~~ | Used | Create Resource, Call Function | |
| PUT | | | | |
| DELETE | | | | |

# (TODO)
### Query String
#### Complex Structure
```javascript
/* Parameter List */
search.xxx.yyy=1
search.xxx.yyy=2
search.zzz=3
```
```javascript
/* qs */
// qs.config()...
```
```java
/* BeanWrapper */
@Data
class SearchDTO {
  Xxx xxx;
  int zzz;

  class Xxx {
    int[] yyy;
  }
}
```

#### Client Library (User-Agent)
```javascript
/* Axios */
const params = { username, password }
axios.get('endpoint', params).then(...)  // GET  + Query (with sencitive data, cachcing)
axios.post('endpoint', params).then(...) // POST + Body (application/json)

const searchParams = new URLSearchParams(params)
axios.get('endpoint', { data: params }).then(...)  // GET  + Body (ignored by XMLHttpRequest.send)
axios.post('endpoint', searchParams).then(...)     // POST + Body (application/x-www-form-urlencoded)
axios.post('endpoint?' + searchParams).then(...)   // POST + Query (without Body)
axios.post('endpoint', null, { params }).then(...) // POST + Query (without Body)

// https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/send
// https://github.com/axios/axios#request-config
// https://github.com/axios/axios/blob/master/lib/adapters/xhr.js#L120
// https://github.com/axios/axios/blob/master/lib/helpers/buildURL.js#L34
// https://github.com/axios/axios/blob/master/lib/defaults.js#L50
```

# References
### Request Methods
> <pre>
>   +---------+-------------------------------------------------+-------+
>   | Method  | Description                                     | Sec.  |
>   +---------+-------------------------------------------------+-------+
>   | GET     | Transfer a current representation of the target | 4.3.1 |
>   |         | resource.                                       |       |
>   | HEAD    | Same as GET, but only transfer the status line  | 4.3.2 |
>   |         | and header section.                             |       |
>   | POST    | Perform resource-specific processing on the     | 4.3.3 |
>   |         | request payload.                                |       |
>   | PUT     | Replace all current representations of the      | 4.3.4 |
>   |         | target resource with the request payload.       |       |
>   | DELETE  | Remove all current representations of the       | 4.3.5 |
>   |         | target resource.                                |       |
> </pre>
> \- _"4.1. Overview", https://tools.ietf.org/html/rfc7231#section-4.1_

### Content-Length
> For example, a Content-Length header field is normally sent in a POST request even when the value is 0 (indicating an empty payload body).
> A user agent SHOULD NOT send a Content-Length header field when the request message does not contain a payload body and the method semantics do not anticipate such a body.
> 
> \- _"3.3.2. Content-Length", https://tools.ietf.org/html/rfc7230#section-3.3.2_

>
> \- _"POST with empty body", https://lists.w3.org/Archives/Public/ietf-http-wg/2010JulSep/0272.html#start_

### Cookie
>
> \- _"", https://developer.mozilla.org/ko/docs/Web/HTTP/Cookies#%EB%B3%B4%EC%95%88_

### CSRF
* OWASP Top 10 (2013), https://owasp.org/www-pdf-archive//OWASP_Top_10_-_2013_Final_-_Korean.pdf
* OWASP Top 10 (2017), https://owasp.org/www-pdf-archive//OWASP_Top_10-2017-ko.pdf

### Query String (Node and Javascript)
* qs, https://www.npmjs.com/package/qs#parsing-arrays
* querystring, https://nodejs.org/api/querystring.html#querystring_querystring_stringify_obj_sep_eq_options
* "Express / Application Settings - query parser", http://expressjs.com/en/api.html#app.settings.table
* "Express / Middleware - body parser", http://expressjs.com/en/resources/middleware/body-parser.html#examples

### Query String (Security)
* "9. Which method is more secure and should be used to deal with sensitive data?",\
https://medium.com/javascript-in-plain-english/get-vs-post-are-you-confident-about-the-differences-189562fac0a7#c629

