# Leaf Simple Auth

## Intro
Setting up a login and sign-up system can sometimes be a very unpleasant experience, especially for new devs. For pro devs, the challenge is "the standard". For this, Leaf has prepared something really simple.

Leaf Leaf Auth allows you to set-up authentication in just one line of code😅😅. Literally 1 line😎. To use Leaf Auth, you simply need to initialise the Leaf Auth package.

```js
$auth = new Leaf\Auth;
```

**Note that `basicLogin`, `basicRegister` and our dev feature `emailLogin` have all been replaced with  simple `login` and `register` methods in v2.**

## Authentication methods:

### login() <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span></sup>
Login is used to create a simple, secure user login. It takes in a table for to search for users(so it's no longer limited to the users table) and a set of parameters for the login.

```js
$user = $auth->login("users", ["username" => "mychi.darko", "password" => md5("test")]);
```

If the user is successfully found, the user data is returned, if not, `false` is returned. You can get any error by calling the `errors` method.

```js
$user = $auth->login("users", [
	"username" => "mychi.darko",
	"password" => md5("test")
]); // returns false if failed

if ($user == false) {
	$response->throwErr($auth->errors());
}
```

example success response:
**Note that the password field is removed**

```js
[
	"id" => 1,
	"username" => "mychi.darko",
	"email" => "mickdd22@gmail.com",
	"created_at" => "2019-09-20 13:47:48",
	"token" => "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE1NzYxMzUzMjgsImlzcyI6ImxvY2FsaG9zdCIsImV4cCI6MTU3NjEzNjIyOCwidXNlcklkIjoxfQ.7FODXGGJKioGQVX4ic0DJLoMIQTVUlsd4zFAJA4DAkg"
]
```

##### Password Encoding
If you use an `md5` encoded password, and the name of your password field is `password`, you can simply leave the password encoding to `login`. For now, only md5 is supported, don't worry, later versions of Leaf will support more encodings.

```js
$user = $auth->login("users", ["username" => "mychi.darko", "password" => "test"], "md5");
```

<hr>

### register() <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span></sup>
Register is a simple method used to create simple, secure user registrations. This option was `basicRegister` in earlier versions. It takes in a table to save users, the params(array) to save.

```js
$auth->register("users", [
	"username" => "mychi.darko",
	"email" => "mickdd22@gmail.com",
	"field" => "value"
]);
```

If the user is successfully saved, the user data is returned, if not, `false` is returned. You can get any error by calling the `errors` method.

```js
$user = $auth->register("users", [
	"username" => "mychi.darko",
	"email" => "mickdd22@gmail.com",
	"field" => "value"
]); // returns false if failed

if ($user == false) {
	$response->throwErr($auth->errors());
}
```


##### Uniques
Let's say you want to check whether the username a user just entered has been taken, you'd have to write a bunch of conditional code, making the code count larger and more error prone, right?

Well, `register` solves this problem smoothly. `register` has a 3rd parameter: an array of unique values which makes sure that the same value can't be saved twice.

```js
$db->register("users", ["name" => "mychi", "email" => "m@m.com", "pass" => "1234"], ["name", "email"]);
```

So, we're telling `register` to alert us if someone has already registered with the name `mychi` or the email `m@m.com`. This is because we passed `["name", "email"]` as the 3rd param to `register`

**With uniques, you can cut down on your whole app:**
For instance, if you know the exact data you'll be receiving in your app, let's say a username, email and password from a register form, you can do something like this:

```js
$leaf->post("/register", function() use($leaf) {
	$leaf->db->register("users", $leaf->request->getBody(), ["username", "email"]);
});
```

So, we pass in the entire request body, which contains the username, email and password. Simple right?

##### Password Encoding
If you use an `md5` encoded password, and the name of your password field is `password`, you can simply leave the password encoding to `register`. For now, only md5 is supported, don't worry, later versions of Leaf will support more encodings.

```js
$leaf->post("/register", function() use($leaf) {
	$leaf->db->register("users", $leaf->request->getBody(), ["username", "email"], "md5");
});
```

<hr>

### [Leaf Authentication Methods](2.0/core/authentication) <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span></sup>

This provides a simple way to work with manual authentication and tokens. All methods here are now available in `Leaf\Auth`, but are only accessible on the `$this` object.

```js
$payload = $this->validate($token);
```

Read [authentication](2.0/core/authentication) for more info

<br>
<hr>

<a href="#/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>