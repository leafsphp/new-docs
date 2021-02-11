# 🕛 Middleware

Middleware are just methods that run before your code runs, be it a particular route or your whole application. Unlike many other frameworks and systems, Leaf gives you the opportunity to set global middleware that run before any and every route.

## ⏳ Before Route Middlewares

Leaf's Core router supports Before Route Middlewares, which are executed before the route handling is processed.

Like route handling functions, you hook a handling function to a combination of one or more HTTP request methods and a specific route pattern.

```php
$app->before('GET|POST', '/admin/.*', function() {
    if (!isset($_SESSION['user'])) {
        header('location: /auth/login');
        exit();
    }
});
```

Unlike route handling functions, more than one before route middleware is executed when more than one route match is found.

## ✨ Before Router Middlewares

Before route middlewares are route specific. Using a general route pattern (viz. all URLs), they can become Before Router Middlewares (in other projects sometimes referred to as before app middlewares) which are always executed, no matter what the requested URL is.

```php
$app->before('GET', '/.*', function() {
    // ... this will always be executed
});
```

## ⌛ After Router Middleware / Run Callback

Run one (1) middleware function, name the After Router Middleware (in other projects sometimes referred to as after app middlewares) after the routing was processed. Just pass it along the $app->run() function. The run callback is route independent.

```php
$app->run(function() { … });
```

Note: If the route handling function has exit()ed the run callback won't be run.

<br>
<hr>

<a href="#/v/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/v/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/v/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>