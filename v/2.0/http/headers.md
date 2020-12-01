# Application Headers

Leaf gives you simple methods to manage both request headers and response headers

## Request Headers

A Leaf application will automatically parse all HTTP request headers. You can directly retrieve the request headers as an array using the `getRequestHeaders` method on the Leaf object.

```php
$leaf->getRequestHeaders();
```

### On the Request object <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span></sup>

You can access the request headers using the request object’s public `headers` property. The `headers` property is an instance of `\Leaf\Helper\Set`, meaning it provides a simple, standardized interface to interactive with the HTTP request headers.

```php
$request = new \Leaf\Http\Request();

// Get request headers as associative array
$headers = $request->headers;

// Get the ACCEPT_CHARSET header
$charset = $request->headers->get('ACCEPT_CHARSET');
```

The HTTP specification states that HTTP header names may be uppercase, lowercase, or mixed-case. Leaf is smart enough to parse and return header values whether you request a header value using upper, lower, or mixed case header name, with either underscores or dashes. So use the naming convention with which you are most comfortable.

<hr>

## Response Headers <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span></sup>

The HTTP response returned to the HTTP client will have a header. The HTTP header is a list of keys and values that provide metadata about the HTTP response. You can use the Leaf application’s response object to set the HTTP response’s header. The response object has a public property `headers` that is an instance of `\Leaf\Helper\Set;` this provides a simple, standardized interface to manipulate the HTTP response headers.

```php
$leaf->response->headers->set('Content-Type', 'application/json');
```

You may also fetch headers from the response object’s `headers` property, too:

```php
$contentType = $leaf->response->headers->get('Content-Type');
```

If a header with the given name does not exist, `null` is returned. You may specify header names with upper, lower, or mixed case with dashes or underscores. Use the naming convention with which you are most comfortable.

### Quick Content-Types

To quickly set the content type of your response, leaf has provided some methods. Currently, there's only support for HTML and JSON, but you'll be seeing better support in future releases.

```php
// Quickly set the content-type of response to html
$leaf->response->headers->contentHtml();

// Quickly set the content-type of response to json
$leaf->response->headers->contentJson();
```

<br>
<hr>

<a href="#/v/2.0/http/response" style="margin: 0px">Response</a>
<a href="#/v/2.0/http/request" style="margin: 0px; 10px;">Request</a>
<a href="#/v/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>