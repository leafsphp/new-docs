<!-- markdownlint-disable no-inline-html -->
# 📢 Leaf Response

The response object is an abstraction of your Leaf application’s HTTP response that is returned to the HTTP client. In v2, the response object has been directly bound to the main Leaf object, so there's no need to instanciate it anymore.

**Note:** Since version 2, `\Leaf\Core\Http\Response` has been shortened to `\Leaf\Http\Response`. Also the response object is available on `$app->response()`.

## 🏂 Using Response

<br>

<div class="alert -warning">
All methods with deprecation warnings have been removed in v2.4 beta
</div>

### 🎄 Response on the Leaf Instance

Since Response is already bound to the Leaf instance, you can do this:

```php
$app = new Leaf\App;

$app->get("/text", function() use($app) {
  $app->response()->respond("This is text");
});
```

Although we've added this, we don't want to force you to do stuff in only one way, so you can still use the `v1.x` method.

### 🎎 Initialising the Response object

With this method, you manually initialise the Response object, and then pass it into your route. Note that in version 2, `\Leaf\Core\Http\Response` has been shortened to `\Leaf\Http\Response`.

```php
$app = new Leaf\App;
$response = new Leaf\Http\Response;

$app->post("/login", function() use($response) {
  // ...
  $response->respond(["username" => $user]);
});
```

An HTTP response has three primary properties:

- Status
- Header
- Body

The response object provides helper methods, described next, that help you interact with these HTTP response properties.

<hr>

## throwErr

"What of error handling?". `throwErr` is just the right method for that. It returns JSON encoded data alongside a code just like `respondWithCode`, however unlike `respondWithCode`, `throwErr` ends the application just like an exception.

You can get more info on http status codes [here](https://www.restapitutorial.com/httpstatuscodes.html).

```php
$app->post('/name', function() use($app) {
  $name = $app->request->get("name");
  if (!$name) $app->response()->throwErr('Name is required', 500);

  // code below won't run since the app breaks on throwErr
});
```

If no code is passed in, throwErr will send a default `500` status code.

**Use message**

Just like with `respondWithCode`, `throwErr` also allows you to use messages instead of codes which most users don't understand.

```php
$response->throwErr("error", 500, true);
```

<hr>

## json

Json, a new method in v2.4 beta, just as the name suggests allows you output json as a reponse. It is supposed to be a replacement for the `respond` and `respondWithCode` methods, as such, comes with the functionality of both of them.

It takes in 4 parameters:

- The data to output
- The https status code of the data, default 200
- Option to show/hide the status code in response body, default `false`
- Option to use message instead of code, default `false`

```php
$response->json("Output", 200);
```

**Output**:

```json
"Output"
```

Showing the code in body:

```php
$response->json("Output", 200, true);
```

**Output**:

```json
{
  "data": "Output",
  "code": 200
}
```

Note that you can't use message and code at the same time

```php
$response->json("Output", 200, true, true);
```

**Output**:

```json
{
  "data": "Output",
  "message": "200 OK"
}
```

<hr>

## page

This is a simple method that outputs a webpage. This method can also be used to achieve server side routing, for example:

```php
$app->get('/homepage', function() use($response) {
  $response->page('link/to/home.html');
});
```

With this, whenever the route `/homepage` is invoked, Leaf loads up `home.html` and outputs it to the user
renderMarkup()

**Note** `page` has **NOTHING** to do with templating, it simply outputs an already defined web page.

For templating with Leaf, [look here](leaf/v/2.4/views/blade/)

**Status Code**

In v2.4 beta, you can add a status code to the page response as the second parameter.

```php
$response->page("404.html", 404);
```

<hr>

## markup

This method outputs a string entered into it as markup with a content type of `text/html`:

For instance, with this code,

```php
$code = "<h2>Hello</h2>";
```

We simply pass it into the response...like this

```php
$app->get('/homepage', function() use($app) {
  $app->response()->markup($code);
});
```

You might be wondering why we don't just use

```php
echo "<h1>hello</h1>";
```

The reason is, Leaf has default headers which set the content type to JSON, in order to correctly output HTML, you need to change this....Leaf has taken care of this with a bunch of other things, all within `markup` and `page`

<hr>

## 🏠 Headers

An instance of `Leaf\Http\Headers` has been included in the response object. This allows you to quickly set response headers without including the Headers package.

```php
$app = new \Leaf\App;
$app->response()->headers->set('Content-Type', 'application/json');
```

You may also fetch `headers` from the response object’s headers property, too:

```php
$contentType = $response->headers->get('Content-Type');
```

If a header with the given name does not exist, `null` is returned. You may specify header names with upper, lower, or mixed case with dashes or underscores. Use the naming convention with which you are most comfortable.

<hr>

## Status

<div class="alert -info">
You can directly set status codes on responses, there's no need to use this method unless you want to use PHP's output methods like <b>echo</b>
</div>

The HTTP response returned to the client will have a status code indicating the response’s type (e.g. 200 OK, 400 Bad Request, or 500 Server Error). You can use the Leaf application’s response object to set the HTTP response’s status like this:

```php
$app->response()->status(400);
```

You only need to set the response object’s status if you intend to return an HTTP response that does not have a 200 OK status. You can just as easily fetch the response object’s current HTTP status by invoking the same method without an argument, like this:

```php
$status = $response->status();
```

<hr>

## 🍪 Cookies

You can also add a cookie using the response object. This uses Leaf Cookies.

### setCookie

This method uses [Leaf Cookie's set](/lucky-charm/http/cookies?id=set)

```php
$app->response()->setCookie("name", "Michael");
```

### simpleCookie

This method uses [Leaf Cookie's simpleCookie](/lucky-charm/http/cookies?id=simplecookie)

```php
$app->response()->simpleCookie("name", "Michael", "1 day");
```

### deleteCookie

This method uses [Leaf Cookie's unset](/lucky-charm/http/cookies?id=unset)

```php
$app->response()->deleteCookie("name");
```

## 🛫cors()

Just a little handy tool especially useful when building APIs. CORS errors are a very common thing for developers who work with APIs, and this method is just a basic bypass for these errors.

This works by setting the `Access-Control-Allow-Headers` and `Access-Control-Allow-Origin` headers with a value of `*` which allows all headers and domains to access content.

```php
$app = new Leaf\App;
$app->response()->cors();

// your code...

$app->run();
```

To specify which origins and headers to allow, you can pass in params into `cors()`

```php
$app->response()->cors("ORIGINS", "HEADERS");
```

**If you end up with cors still shouting at you because of OPTIONS requests, you can use:**

```php
$app->evadeCors(true, "ORIGINS", "HEADERS");
```

<br>
<hr>

<a href="#/v/2.0/http/response" style="margin: 0px">Response</a>
<a href="#/v/2.0/http/session" style="margin: 0px 10px;">Session</a>
<a href="#/v/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
