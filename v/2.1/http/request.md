# 🧿 Leaf Request

The request object is an abstraction of the current HTTP request and allows you to easily interact with any data passed into your application. In v2.0, the request object has been directly bound to the main Leaf object, so there's no need to instanciate it anymore.

**Note:** In version 2, `\Leaf\Http\Request` has been shortened to `\Leaf\Http\Request`. Also the request object is available on `$leaf->request`.

## Using Request

### 🎄 Request on the Leaf Instance

Since Request is already bound to the Leaf instance, you can do this:

```php
$leaf = new Leaf\App();

$leaf->post("/user/change-username", function() use($leaf) {
  echo $leaf->response->get("username");
});
```

Although we've added this, we don't want to force you to do stuff in only one way, so you can still use the `v1.x` method.

### 🎪 Initialising the Request object

With this method, you manually initialise the Request object, and then pass it into your route. Note that in version 2, `\Leaf\Http\Request` has been shortened to `\Leaf\Http\Request`.

```php
$leaf = new Leaf\App();
$request = new Leaf\Http\Request();

$leaf->post("/items/add", function() use($request) {
  echo $request->get("username");
});
```

## 📖 Basic Usage

### get()

`get()` is a general purpose method which retrieves a particular item from the request body. In simpler terms, it works like `$_POST['key']` but works for all request types. It takes in one parameter: the key of the parameter you wish to get.

```php
$leaf->post('/name/add', function() use($leaf) {
  $name = $leaf->request->get('name');
});

// get: linkToApp?id=1
$id = $leaf->request->get('id');
```

#### Security Fixes

`get()` has also received a bunch of security fixes which prevent maliscious scripts from being passed into your application.

<hr>

### body()

**Previously `getBody()`**

`body()` is another general purpose method which retrieves the key => value pairs of the entire request body. In simpler terms, it works like `$_POST` but works for all request types.

```php
$leaf->post('/name/add', function() use($leaf) {
  $body = $leaf->request->body();
});
```

#### 🧐 Security Fixes

`body()` has also received a bunch of security fixes which prevent maliscious scripts from being passed into your application.

<hr>

## Headers

A Leaf application will automatically parse all HTTP request headers. You can access the request headers using the request object’s public headers property. The headers property is an instance of \Leaf\Helper\Set, meaning it provides a simple, standardized interface to interactive with the HTTP request headers.

```php
<?php
$leaf = new \Leaf\App();

// Get request headers as associative array
$headers = $leaf->request->headers;

// Get the ACCEPT_CHARSET header
$charset = $leaf->request->headers->get('ACCEPT_CHARSET');
```

The HTTP specification states that HTTP header names may be uppercase, lowercase, or mixed-case. Leaf is smart enough to parse and return header values whether you request a header value using upper, lower, or mixed case header name, with either underscores or dashes. So use the naming convention with which you are most comfortable.

<hr>

## Request Method

Every HTTP request has a method (e.g. GET or POST). You can obtain the current HTTP request method via the Leaf application’s request object:

```php
/**
 * What is the request method?
 * @return string (e.g. GET, POST, PUT, DELETE)
 */
$leaf->request->getMethod();

/**
 * Is this a GET request?
 * @return bool
 */
$leaf->request->isGet();

/**
 * Is this a POST request?
 * @return bool
 */
$leaf->request->isPost();

/**
 * Is this a PUT request?
 * @return bool
 */
$leaf->request->isPut();

/**
 * Is this a DELETE request?
 * @return bool
 */
$leaf->request->isDelete();

/**
 * Is this a HEAD request?
 * @return bool
 */
$leaf->request->isHead();

/**
 * Is this a OPTIONS request?
 * @return bool
 */
$leaf->request->isOptions();

/**
 * Is this a PATCH request?
 * @return bool
 */
$leaf->request->isPatch();

/**
 * Is this a XHR/AJAX request?
 * @return bool
 */
$leaf->request->isAjax();
```

<hr>

## XHR

When using a Javascript framework like MooTools or jQuery to execute an XMLHttpRequest, the XMLHttpRequest will usually be sent with a **X-Requested-With** HTTP header. The Leaf application will detect the HTTP request’s **X-Requested-With** header and flag the request as such. If for some reason an XMLHttpRequest cannot be sent with the **X-Requested-With** HTTP header, you can force the Leaf application to assume an HTTP request is an XMLHttpRequest by setting a GET, POST, or PUT parameter in the HTTP request named “isajax” with a truthy value.

Use the request object’s `isAjax()` or `isXhr()` method to tell if the current request is an XHR/Ajax request:

```php
$isXHR = $leaf->request->isAjax();
$isXHR = $leaf->request->isXhr();
```

<hr>

## Helpers

The Leaf application’s request object provides several helper methods to fetch common HTTP request information:

### Content Type

Fetch the request’s content type (e.g. “application/json;charset=utf-8”):

```php
<?php
$leaf->request->getContentType();
```

### Media Type

Fetch the request’s media type (e.g. “application/json”):

```php
<?php
$leaf->request->getMediaType();
```

### Media Type Params

Fetch the request’s media type parameters (e.g. [charset => “utf-8”]):

```php
<?php
$leaf->request->getMediaTypeParams();
```

### Content Charset

Fetch the request’s content character set (e.g. “utf-8”):

```php
<?php
$leaf->request->getContentCharset();
```

### Content Length

Fetch the request’s content length:

```php
<?php
$leaf->request->getContentLength();
```

### Host

Fetch the request’s host (e.g. “leafphp.netlify.com”):

```php
<?php
$leaf->request->getHost();
```

### Host with Port

Fetch the request’s host with port (e.g. “leafphp.netlify.com:80”):

```php
<?php
$leaf->request->getHostWithPort();
```

### Port

Fetch the request’s port (e.g. 80):

```php
<?php
$leaf->request->getPort();
```

### Scheme

Fetch the request’s scheme (e.g. “http” or “https”):

```php
<?php
$leaf->request->getScheme();
```

### Path

Fetch the request’s path (root URI + resource URI):

```php
<?php
$leaf->request->getPath();
```

### URL

Fetch the request’s URL (scheme + host [ + port if non-standard ]):

```php
<?php
$leaf->request->getUrl();
```

### IP Address

Fetch the request’s IP address:

```php
<?php
$leaf->request->getIp();
```

### Referer

Fetch the request’s referrer:

```php
<?php
$leaf->request->getReferrer();
```

### User Agent

Fetch the request’s user agent string:

```php
<?php
$leaf->request->getUserAgent();
```

<hr>

## Paths

Every HTTP request received by a Leaf application will have a root URI and a resource URI.

### Root URI

The root URI is the physical URL path of the directory in which the Leaf application is instantiated and run. If a Leaf application is instantiated in **index.php** within the top-most directory of the virtual host’s document root, the root URI will be an empty string. If a Leaf application is instantiated and run in **index.php** within a physical subdirectory of the virtual host’s document root, the root URI will be the path to that subdirectory with a leading slash and without a trailing slash.

### Resource URI

The resource URI is the virtual URI path of an application resource. The resource URI will be matched to the Leaf application’s routes.

Assume the Leaf application is installed in a physical subdirectory **/foo** beneath your virtual host’s document root. Also assume the full HTTP request URL (what you’d see in the browser location bar) is **/foo/books/1**. The root URI is /foo (the path to the physical directory in which the Leaf application is instantiated) and the resource URI is **/books/1** (the path to the application resource).

You can get the HTTP request’s root URI and resource URI with the request object’s `getRootUri()` and `getResourceUri()` methods:

```php
$leaf = new \Leaf\App();

//Get root URI
$rootUri = $leaf->request->getRootUri();

//Get resource URI
$resourceUri = $leaf->request->getResourceUri();
```

<br>
<hr>

<a href="#/v/2.1/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/v/2.1/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/2.1/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.1/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>