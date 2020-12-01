# 📲 Routing

As explained [before](v/lucky-charm/intro/htaccess), Leaf uses a single root file, to which all the server requests are redirected. Leaf then takes these requests and matches them to rules you have defined. The results are then displayed to the user. It's actually a very simple concept.

The router module is tied directly to Leaf Core, so once you initialise leeaf, you can use routing

```php
$app = new Leaf\App;
```

## 👋 Using a different router

Although Leaf provides you with a default router, you are free to import and use any router you want.

1. Install whatever you want

```bash
composer require imaginary/router
```

2. Import and use it in your project

```php
$app = new Leaf\App;
// initialise imaginary router
$imr = new Imaginary\Router();
// you can still use leaf modules
$imr->get("/", function() use($app) {
  $app->response->respond(["title" => "hello"]);
});
```

## ⛳ Creating Routes

Back to Leaf's router, You can define application routes using proxy methods on the Leaf\App instance. Leaf supports different types of requests, let's look at them.

### GET

You can add a route that handles only GET HTTP requests with the Leaf router's get() method. It accepts two arguments:

- The route pattern (with optional named placeholders or PCRE based patterns)
- The route callback

```php
$app->get('/home', function() {
  // your code
});
```

### POST

You can add a route that handles only POST HTTP requests with the Leaf router's post() method. It accepts two arguments:

- The route pattern (with optional named placeholders or PCRE based patterns)
- The route callback

```php
$app->post('/users/add', function() use($request) {
  $user = $request->get('user');
  // create a new user
});
```

Using Post Params
View [Request](v/lucky-charm/http/request) for more info on handling params

### PUT requests

You can add a route that handles only PUT HTTP requests with the Leaf router’s put() method. It accepts two arguments:

- The route pattern (with optional named placeholders or PCRE based patterns)
- The route callback

```php
$app->put('/book/edit/{id}', function($id) {
  // your code
});
```

### DELETE requests

You can add a route that handles only DELETE HTTP requests with the Leaf router's delete() method. It accepts two arguments:

- The route pattern (with optional named placeholders or PCRE based patterns)
- The route callback

```php
$app->delete('/quotes/{id}', function($id) {
  // delete quote
});
```

### OPTIONS requests

You can add a route that handles only OPTIONS HTTP requests with the Leaf router's options() method. It accepts two arguments:

- The route pattern (with optional named placeholders or PCRE based patterns)
- The route callback

```php
$app->options('/quotes/{id}', function($id) {
  // return headers
});
```

### PATCH requests

You can add a route that handles only PATCH HTTP requests with the Leaf router's patch() method. It accepts two arguments:

- The route pattern (with optional named placeholders or PCRE based patterns)
- The route callback

```php
$app->patch('/post/{id}', function($id) {
  // your code
});
```

### ALL requests

You can add a route that handles all HTTP requests with the Leaf router's all() method. It accepts two arguments:

- The route pattern (with optional named placeholders or PCRE based patterns)
- The route callback

```php
$app->all('/post/{id}', function($id) {
  // your code
});
```

### Resource Routes

This section assumes you've read [working with controllers](v/lucky-charm/routing/controller). In an MVC application, controllers play a major role as they're the bridge between your view and your model.

A resource route simply creates all the routes needed to successfully handle a particular feature. This sounds a bit bleak, let's look at an example.

```php
$app = new Leaf\App;

$app->resource("/posts", "PostsController");

$app->run();
```

The code above is equivalent to this:

```php
$app = new Leaf\App;

$this->match("GET|HEAD", "/posts", "$controller@index");
$this->post("/posts", "$controller@store");
$this->match("GET|HEAD", "/posts/create", "$controller@create");
$this->match("POST|DELETE", "/posts/{id}/delete", "$controller@destroy");
$this->match("POST|PUT|PATCH", "/posts/{id}/edit", "$controller@update");
$this->match("GET|HEAD", "/posts/{id}/edit", "$controller@edit");
$this->match("GET|HEAD", "/posts/{id}", "$controller@show");

$app->run();
```

Resource routes are handled by a [resource controller](v/lucky-charm/routing/controller?id=resource-controller).

### Route "Hooking"

You can add a route that handles a couple of HTTP methods with the Leaf router's match() method. It accepts three arguments:

- The HTTP method(s) seperated by |
- The route pattern (with optional named placeholders or PCRE based patterns)
- The route callback

```php
$app->match('GET|POST', '/people', function() {
  // your code
});
```

### Running your routes

After setting all the routes, you'll need to dispatch the routes. This is achieved through Leaf's run() method.

```php
$app->run();
```

<hr>

# Handling 404

Leaf's core router has specially prepared for 404 errors, and is bent on giving users full control over displaying this error

For this reason, we've prepared the set404() method. In version 2, you can just call set404 without passing in any function, this will set the 404 handler to the default Leaf 404 page. You can change this at any time by passing in your custom page

```php
// will use default Leaf 404 page(new in v2.0)
$app->set404();

// custom 404 page
$app->set404(function() use($app) {
  $app->response->renderPage("./pages/404.html");
});
```

<br>
<hr>

<a href="#/v/lucky-charm/http/request" style="margin: 0px">Request</a>
<a href="#/v/lucky-charm/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/v/lucky-charm/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/lucky-charm/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/lucky-charm/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>