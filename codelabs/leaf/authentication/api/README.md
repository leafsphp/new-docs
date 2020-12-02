# API Authentication (v2.4 Beta)

## Version support

This experiment supports `v2.4-beta` upwards.

## Base Example

Modern web app conventions have led to a lot of web apps relying on AJAX requests to a backend (API) using libraries like [axios](https://github.com/axios/axios). These backend APIs take in json encoded data from the frontend, perform some operations and send back a response.

In this experiment, we'll be looking at how to create logins, signups and user updates with Leaf v2.4 beta. We'll have various requests in JSON form, and some with headers which we'll be using for this experiment.

## Building Our Login

In a "realworld app", such data is usually submitted to an [API endpoint](https://smartbear.com/learn/performance-monitoring/api-endpoints/) or route, so of course, we'll have to setup a handler.

We'll use leaf's core router for this.

```php
require "vendor/autoload.php";

$app = new Leaf\App;

$app->post("/login", function() use($app) {
  // login stuff here
});

$app->run();
```

Before we jump into the code, let's talk about the processes involved in modern API logins. APIs are **usually** powered by JWT which have some user data encoded into them. These tokens are used to verify a user's login status as well as get information about the user.

This means that we would have to generate a JWT, not forgetting to retrieve the data from the database. All this sounds pretty complex, but Leaf allows us to do all of this in just one line of code. Yes, just one line.

Let's take a look at our JSON payload.

```js
{
  "username": "mychi",
  "password": "testing123"
}
```

So our user's username and password are passed into our app, we first need to retrieve these from the request. It's a lot easier with `v2.4-beta`.

```php
$data = $app->request()->get(["username", "email"]);
```

This grabs the username and email from the request and saves them in the `$data` variable. After that, we will need to tackle the part that checks the database for the current credentials and generates a JWT if the user is found. Before, we can work wit our database, we need to connect to it:

```php
$auth = new Leaf\Auth;
$auth->connect("host", "user", "password", "dbName");
```

Now that we're done with that, let's check our database and generate our token. Here's our one line of code😂

```php
$payload = $auth->login("users", $data);
```

By default, Leaf will use `md5` to encode the password before comparing in the database. It might be fine for simple use cases, but sometimes you might want a more complex hashing algorithm. [Auth Settings](v/2.4-beta/core/auth?id=auth-config-small-classnew-tag-1new) allow us to customize the way Auth behaves. We can also set a custom password hash.

```php
$auth->config("PASSWORD_ENCODE", function($password) {
  return \CustomPasswordHash::create($password);
});
```

Putting all of this together, we'll have something like this:

```php
require "vendor/autoload.php";

$app = new Leaf\App;
$auth = new Leaf\Auth;

$auth->connect("host", "user", "password", "dbName");
$auth->config("PASSWORD_ENCODE", function($password) {
  return \CustomPasswordHash::create($password);
});

$app->post("/login", function() use($app, $auth) {
  $data = $app->request()->get(["username", "email"]);
  $payload = $auth->login("users", $data);

  if (!$payload) {
    $app->response()->throwErr($auth->errors());
  }

  $app->response()->json($payload);
});

$app->run();
```

The output will look like this:

```js
{
  "user": {
    "username": "mychi",
    "email": "mickdd22@gmail.com",
    "created_at": "2019-09-20 13:47:48"
  },
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE1NzYxMzUzMjgsImlzcyI6ImxvY2FsaG9zdCIsImV4cCI6MTU3NjEzNjIyOCwidXNlcklkIjoxfQ.7FODXGGJKioGQVX4ic0DJLoMIQTVUlsd4zFAJA4DAkg"
}
```

It's this easy to create logins, so what about registrations? Even easier. Registration involvessaving the user in the database, if the user is returned immedietely, a token needs to be created as well. Since we've already configured Leaf Auth, let's just jump right into the code.

```php
$app->post("/register", function() use($app, $auth) {
  $data = $app->request()->get(["username", "email", "password"]);
  $payload = $auth->register("users", $data, ["username", "email"]);

  if (!$payload) {
    $app->response()->throwErr($auth->errors());
  }

  $app->response()->json($payload);
});
```

Here, we're creating a handler for our register method, getting the request data we need and saving it in the database using `register`. You might have noticed the 3rd parameter, `["username", "email"]`. This just makes sure that the same username and email don't already exist in the database. Leaf literally does everything for you. Now let's move on to editing the user.

To edit a user, we have to find the user we want to edit. This means that the user should be logged in. Since we're using JWT, we'll need to pass the token into the request as a bearer token in the authorization header.

An example of this with axios will look like this:

```js
import axios from "axios";

axios({
  url: `${API_URL}/update`,
  method: "POST",
  headers: {
    Authorization: `Bearer ${token}`,
  },
  ...
})
```

Back on our system, we'll have to detect the token, grab and decode it, find the data encoded into it and retrieve the user id. Sounds complex, but again, one line of code with Leaf.

```php
$userId = $auth->id() ?? $app->response()->throwErr($auth->errors());
```

Based on this id, we can create a condition to find the user we want to update. This condition will be passed together with our params into the `update` method, which will look like this:

```php
$data = $request->get(["username", "email"]);

// credentials to find user by
$where = ["id" => $auth->id() ?? $app->response()->throwErr($auth->errors())];

// unique data
$uniques = ["username", "email"];

// validation
$validation = ["username" => "ValidUsername", "email" => "email"];

$user = $auth->update("users", $data, $where, $uniques, $validation);
```

<br>

Experiment by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
