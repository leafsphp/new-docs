<!-- markdownlint-disable no-inline-html -->
# ✨ Leaf Simple Auth

## Intro

Setting up a login and sign-up system can sometimes be a very unpleasant experience, especially for new devs. For pro devs, the challenge is "the standard". For this, Leaf has prepared something really simple.

Leaf Auth allows you to set-up authentication in just one line of code😅😅. Literally 1 line😎. To use Leaf Auth, you simply need to initialise the Leaf Auth package.

```php
$auth = new Leaf\Auth;
```

## Authentication methods

### login

Login is used to create a simple, secure user login. It takes in a table to search for users(so it's no longer limited to the users table) and a set of parameters for the login.

```php
$user = $auth->login("users", [
  "username" => "mychi.darko",
  "password" => md5("test")
]);
```

If the user is successfully found, the user data is returned, if not, `false` is returned. You can get any error by calling the `errors` method.

```php
$user = $auth->login("users", [
  "username" => "mychi.darko",
  "password" => md5("test")
]); // returns false if failed

if ($user == false) {
  $response->throwErr($auth->errors());
}
```

example success response:
**Note that the password and id fields are removed**

```php
[
  "username" => "mychi.darko",
  "email" => "mickdd22@gmail.com",
  "created_at" => "2019-09-20 13:47:48",
  "token" => "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE1NzYxMzUzMjgsImlzcyI6ImxvY2FsaG9zdCIsImV4cCI6MTU3NjEzNjIyOCwidXNlcklkIjoxfQ.7FODXGGJKioGQVX4ic0DJLoMIQTVUlsd4zFAJA4DAkg"
]
```

**In v2.2, the `id` field is also hidden if is present.**

#### Password Encoding

If you use an `md5` encoded password, and the name of your password field is `password`, you can simply leave the password encoding to `login`. For now, only md5 is supported, don't worry, later versions of Leaf will support more encodings.

```php
$user = $auth->login("users", ["username" => "mychi.darko", "password" => "test"], "md5");
```

#### Default Checks

Generally speaking, most logins/signups require a (username/email) + password combination, default checks allow you to validate data entered into these fields without you having to write any validation yourself.

Default checks look for a `username` field and test it against the [ValidUsername](lucky-charm/core/forms?id=validate) rule, an `email` against the [email](lucky-charm/core/forms?id=validate) rule and a `password` field against the [required](lucky-charm/core/forms?id=validate) rule.

To use default checks, you simply have to pass `true` as the 4th parameter to login

```php
$user = $auth->login("users", [
  "username" => "mychi.darko",
  "password" => "test"
], "md5", true);
```

To get any errors, you need to call the `errors` method

```php
$user = $auth->login("users", [
  "username" => "mychi.darko",
  "password" => "test"
], "md5", true);

if ($user == false) {
  $app->response->throwErr($auth->errors());
}
```

<hr>

### register()

Register is a simple method used to create simple, secure user registrations. This option was `basicRegister` in earlier versions. It takes in a table to save users, the params(array) to save.

```php
$auth->register("users", [
  "username" => "mychi.darko",
  "email" => "mickdd22@gmail.com",
  "field" => "value"
]);
```

If the user is successfully saved, the user data is returned, if not, `false` is returned. You can get any error by calling the `errors` method.

```php
$user = $auth->register("users", [
  "username" => "mychi.darko",
  "email" => "mickdd22@gmail.com",
  "field" => "value"
]); // returns false if failed

if ($user == false) {
  $response->throwErr($auth->errors());
}
```

#### Uniques

Let's say you want to check whether the username a user just entered has been taken, you'd have to write a bunch of conditional code, making the code count larger and more error prone, right?

Well, `register` solves this problem smoothly. `register` has a 3rd parameter: an array of unique values which makes sure that the same value can't be saved twice.

```php
$db->register("users", ["name" => "mychi", "email" => "m@m.com", "pass" => "1234"], ["name", "email"]);
```

So, we're telling `register` to alert us if someone has already registered with the name `mychi` or the email `m@m.com`. This is because we passed `["name", "email"]` as the 3rd param to `register`

**With uniques, you can cut down on your whole app:**
For instance, if you know the exact data you'll be receiving in your app, let's say a username, email and password from a register form, you can do something like this:

```php
$app->post("/register", function() use($app) {
  $auth->register("users", $app->request->getBody(), ["username", "email"]);
});
```

So, we pass in the entire request body, which contains the username, email and password. Simple right?

#### Password Encoding

If you use an `md5` encoded password, and the name of your password field is `password`, you can simply leave the password encoding to `register`. For now, only md5 is supported, don't worry, later versions of Leaf will support more encodings.

```php
$app->post("/register", function() use($app) {
  $auth->register("users", $app->request->getBody(), ["username", "email"], "md5");
});
```

#### Default Checks

Generally speaking, most logins/signups require a (username/email) + password combination, default checks allow you to validate data entered into these fields without you having to write any validation yourself.

Default checks look for a `username` field and test it against the [ValidUsername](lucky-charm/core/forms?id=validate) rule, an `email` against the [email](lucky-charm/core/forms?id=validate) rule and a `password` field against the [required](lucky-charm/core/forms?id=validate) rule.

To use default checks, you simply have to pass `true` as the 5th parameter to login

```php
$auth->register("users", $app->request->getBody(), ["username", "email"], "md5", true);
```

To get any errors, you need to call the `errors` method

```php
if ($auth->register("users", $app->request->getBody(), ["username", "email"], "md5", true) == false) {
  $app->response->throwErr($auth->errors());
}
```

<hr>

### currentUser <sup class="new-tag-1">New in Lucky Charm🍀</sup>

When tokens are added inside requests, you generally have to decode the token and query your database with the id returned to get the current user. Although Leaf Auth makes it really simple, it can get even simpler; by calling a single method. It takes in one parameter, the table to look for users.

```php
$user = $auth->currentUser("users");
return $user["name"];
```

In Lucky Charm, the table is set to `users` by default. So you can simply do this:

```php
$user = $auth->currentUser();
```

<hr>

### useToken <sup class="new-tag-1">New in Lucky Charm🍀</sup>

This is a method that decodes a token and returns the `user_id` field encoded in it.

```php
$user_id = $auth->useToken();
```

<hr>

### [Leaf Authentication Methods](lucky-charm/core/authentication)

Leaf Auth now uses the `Leaf\Helpers\Authentication` package to provide solutions for token authentication. This provides a simple way to work with manual authentication and tokens. All methods here are now available in `Leaf\Auth`.

```php
$payload = $auth->validate($token);
```

Read [authentication](lucky-charm/core/authentication) for more info

<hr>

### Token Secrets

Token Secrets are basically simple `strings` which are encoded into your Tokens to prevent others from logging into accounts with fake tokens. You simply need to set your own token secrets while encoding and decoding tokens.

#### Basic Usage

```php
$auth->setSecretKey('tH1$_iS_MY_$3¢Ret');

$auth->token->generateSimpleToken($user_id, $auth->getSecretKey());
```

<br>
<hr>

<a href="#/lucky-charm/http/request" style="margin: 0px">Request</a>
<a href="#/lucky-charm/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/lucky-charm/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/lucky-charm/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/lucky-charm/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
