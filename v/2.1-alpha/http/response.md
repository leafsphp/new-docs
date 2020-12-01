# Leaf Response
The response object is an abstraction of your Leaf application’s HTTP response that is returned to the HTTP client. In v2.0, the response object has been directly bound to the main Leaf object, so there's no need to instanciate it anymore. 

**Note:** In version 2, `\Leaf\Http\Response` has been shortened to `\Leaf\Http\Response`. Also the response object is available on `$leaf->response`.

## Using Response
### Response on the Leaf Instance 
Since Response is already bound to the Leaf instance, you can do this:
```php
$leaf = new Leaf\App();

$leaf->get("/text", function() use($leaf) {
	$leaf->response->respond("This is text");
});
```
Although we've added this, we don't want to force you to do stuff in only one way, so you can still use the `v1.x` method.

### Initialising the Response object
With this method, you manually initialise the Response object, and then pass it into your route. Note that in version 2, `\Leaf\Http\Response` has been shortened to `\Leaf\Http\Response`.
```php
$leaf = new Leaf\App();
$response = new Leaf\Http\Response();

$leaf->post("/login", function() use($response) {
	...
	$response->respond(["username" => $user]);
});
```

An HTTP response has three primary properties:

- Status
- Header
- Body

The response object provides helper methods, described next, that help you interact with these HTTP response properties.

<hr>

## respond()
Respond is a general purpose method that returns JSON encoded data to the user.

```php
$leaf->get('/', function() use($leaf) {
  	$leaf->response->respond(["message" => "something"]);
});
```

<hr>

## Status 
The HTTP response returned to the client will have a status code indicating the response’s type (e.g. 200 OK, 400 Bad Request, or 500 Server Error). You can use the Leaf application’s response object to set the HTTP response’s status like this:

```php
$leaf->response->setStatus(400);
```

You only need to set the response object’s status if you intend to return an HTTP response that does not have a 200 OK status. You can just as easily fetch the response object’s current HTTP status by invoking the same method without an argument, like this:
```php
$status = $leaf->response->getStatus();
```

<hr>

## respondWithCode()
`setStatus` set's the status of your response, and can be used with any of the other response methods, however, it doesn't return any data to the user. `respondWithCode` solves this problem. It returns json encoded data to the user with a response status.

```php
// response with 400 status
$leaf->response->respondWithCode(["message" => "something"], 400);

// response with 200 status
$leaf->response->respondWithCode(["message" => "something"]);
```

## throwErr()
"What of error handling?". `throwErr` is just the right method for that. It returns JSON encoded data along side a code just like `respondWithCode`, however unlike `respondWithCode`, `throwErr` ends the application just like an exception.
You can get more info on http status codes [here](https://www.restapitutorial.com/httpstatuscodes.html)

```php
$leaf->post('/name', function() use($leaf) {
	$name = get("name");
	$name ==  null ? $leaf->response->throwErr('Name is null', $code) : null;
});
```

<hr>

## Headers 
The HTTP response returned to the HTTP client will have a header. The HTTP header is a list of keys and values that provide metadata about the HTTP response. You can use the Leaf application’s response object to set the HTTP response’s header. The response object has a public property `headers` that is an instance of `\Leaf\Helper\Set`; this provides a simple, standardized interface to manipulate the HTTP response headers.
```php
$leaf = new \Leaf\App();
$leaf->response->headers->set('Content-Type', 'application/json');
```

You may also fetch `headers` from the response object’s headers property, too:
```php
$contentType = $leaf->response->headers->get('Content-Type');
```
If a header with the given name does not exist, `null` is returned. You may specify header names with upper, lower, or mixed case with dashes or underscores. Use the naming convention with which you are most comfortable.

<hr>

## renderPage()
This is a simple method that outputs a webpage. This method can also be used  to achieve server side routing, for example:
```php
$leaf->get('/homepage', function() use($response) {
  	$leaf->response->renderPage('link/to/home.html');
});
```
With this, whenever the route `/homepage` is invoked, Leaf loads up `home.html` and outputs it to the user
renderMarkup()

**Note** `renderPage` has **NOTHING** to do with templating, it simply outputs an already defined web page.

For templating with Leaf, [look here](2.1templating/)

<hr>

## renderMarkup()
This method outputs a string entered into it as markup with a content type of `text/html`:

For instance, with this code,
```php
$code = "<h2>Hello</h2>";
```
We simply pass it into the response...like this

```php
$leaf->get('/homepage', function() use($leaf) {
  $leaf->response->renderMarkup($code);
});
```
You might be wondering why we don't just use
```php
echo "<h1>hello</h1>";
```
The reason is, Leaf has default headers which set the content type to JSON, in order to correctly output HTML, you need to change this....Leaf has taken care of this with a bunch of other things, all within `renderMarkup` and `renderPage`

<hr>

## Helpers 
The response object provides helper methods to inspect and interact with the underlying HTTP response.

### Finalize
The response object’s `finalize()` method returns a numeric array of `[status, header, body]`. The status is an integer; the header is an iterable data structure; and the body is a string. Were you to create a new \Leaf\Http\Response object in your Leaf application or its middleware, you would call the response object’s `finalize()` method to produce the status, header, and body for the underlying HTTP response.

```php
<?php
/**
 * Prepare new response object
 */
$leaf->response->setStatus(400);
$leaf->response->write('You made a bad request');
$leaf->response->headers->set('Content-Type', 'text/plain');

/**
 * Finalize
 * @return [
 *     200,
 *     ['Content-type' => 'text/plain'],
 *     'You made a bad request'
 * ]
 */
$array = $leaf->response->finalize();
```

### Status Introspection
The response object provides other helper methods to inspect its current status. All of the following methods return a boolean value:

```php
//Is this an informational response?
$leaf->response->isInformational();

//Is this a 200 OK response?
$leaf->response->isOk();

//Is this a 2xx successful response?
$leaf->response->isSuccessful();

//Is this a 3xx redirection response?
$leaf->response->isRedirection();

//Is this a specific redirect response? (301, 302, 303, 307)
$leaf->response->isRedirect();

//Is this a forbidden response?
$leaf->response->isForbidden();

//Is this a not found response?
$leaf->response->isNotFound();

//Is this a client error response?
$leaf->response->isClientError();

//Is this a server error response?
$leaf->response->isServerError();
```

<br>
<hr>

<a href="#/v/2.1-alpha/http/response" style="margin: 0px">Response</a>
<a href="#/v/2.1-alpha/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/2.1-alpha/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.1-alpha/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>