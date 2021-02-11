<!-- markdownlint-disable no-inline-html -->
# ✨ Leaf Simple Auth

## Intro

Setting up a login and sign-up system can sometimes be a very unpleasant experience, especially for new devs. For pro devs, the challenge is "the standard". For this, Leaf has prepared something really simple.

Leaf Auth allows you to set-up authentication in just one line of code😅😅. Literally 1 line😎. To use Leaf Auth, you simply need to initialise the Leaf Auth package.

```php
$auth = new Leaf\Auth;
```

After initializing Auth, you need to connect it to your database, you can add your db credentials in `connect` or use `autoConnect` if you've already configured your database in your `.env` file.

```php
$auth->connect("host", "user", "password", "dbname");
// or
$auth->autoConnect();
```

## Auth Config

Auth Config was added in v2.4-beta to give you more control over how leaf handles authentication in your apps. Auth has been configured perfectly for most apps, but not all use cases are the same, hence, this brilliant addition.

This also includes various configurations for doing things like:

- Setting custom token lifetime
- Hiding/Showing user fields
- Adding/removing default timestamps
- Changing the default password key
- Setting custom password encode methods
- Turning off password encoding totally
- Setting custom password verify methods (NEW)
- Hiding/Showing password field (NEW)
- Adding custom validation messages (NEW)

### config

To set a config variable, you can simply call the `config` method.

```php
$auth->config("item", "value");
```

### Settings

- **USE_TIMESTAMPS:** This determines whether Leaf should add the default `created_at` and `updated_at` timestamps on register and update. Default is `true`.
- **PASSWORD_ENCODE** *This method has gone through a lot of changes since v2.4 beta, and may not work exactly the same way*. This setting is run when leaf wants to encode a password. It now uses `PASSWORD_DEFAULT` by defaullt for encryption.

```php
// This turns off password encoding
$auth->config("PASSWORD_ENCODE", false);

// defult encoding (Leaf\Helpers\Password::hash)
$auth->config("PASSWORD_ENCODE", null);

// use md5. We're still keeping support for md5 :-)
$auth->config("PASSWORD_ENCODE", Password::MD5);

// use custom method
$auth->config("PASSWORD_ENCODE", function($password) {
  return Password::hash($password);
});
```

- **<small class="new-tag-1">New</small> PASSWORD_VERIFY** This setting is called when Leaf tries to verify a password. It works just like `PASSWORD_ENCODE` above.

```php
// This turns off password encoding
$auth->config("PASSWORD_VERIFY", false);

// defult encoding (Leaf\Helpers\Password::hash)
$auth->config("PASSWORD_VERIFY", null);

// use md5. We're still keeping support for md5 :-)
$auth->config("PASSWORD_VERIFY", Password::MD5);

// use custom method
$auth->config("PASSWORD_VERIFY", function($password) {
  return Password::verify($password);
});
```

- **PASSWORD_KEY** allows you to change the password field name, maybe your's is passcode?

```php
$auth->config("PASSWORD_KEY", "passcode");
```

- **HIDE_ID** takes in a boolean, and determines whether to hide the id in the user object.

- **<small class="new-tag-1">New</small> HIDE_PASSWORD** Just as the name implies, allows you to hide or show the password in the final results returned from auth.

- **<small class="new-tag-1">New</small> LOGIN_PARAMS_ERROR** This is the error to show if there's an error with any parameter which isn't the password eg: username:

```php
$auth->config("LOGIN_PARAMS_ERROR", "Username is incorrect!");
```

- **<small class="new-tag-1">New</small> LOGIN_PASSWORD_ERROR** This is the error to show if there's an error with the password

```php
$auth->config("LOGIN_PASSWORD_ERROR", "Password is incorrect!");
```

- **<small class="new-tag-1">New</small> USE_SESSION** Use session based authentication instead of the default JWT based auth. Without this setting enbled, you can't use any of the session methods below.

- **<small class="new-tag-1">New</small> SESSION_ON_REGISTER** If true, a session will be created on a successful registration, else you it'll be created on login rather.

- **<small class="new-tag-1">New</small> GUARD_LOGIN** The page route.

- **<small class="new-tag-1">New</small> GUARD_REGISTER** The register page route.

- **<small class="new-tag-1">New</small> GUARD_LOGOUT** Logout route handler.

- **<small class="new-tag-1">New</small> GUARD_HOME** Home page route.

- **<small class="new-tag-1">New</small> SAVE_SESSION_JWT** Add an auth token to the auth session? This allows you save a generated JWT to the session. You might want to use this if you want to extend your app into an API.

### tokenLifetime

This method allows you to get or set the token lifetime value. In previous versions, the lifetime value was set by leaf, here you can customize it the way you want to.

```php
// change token lifetime
$auth->tokenLifetime(24 * 24 * 24);

// get token lifetime
$lifetime = $auth->tokenLifetime();
```

## Session support <sup class="new-tag-1">New in v2.4.1</sup>

Leaf auth finally includes support for session based authentication in this version. Session based authentication as the name implies creates and manages a session during the authentication to manage the user's logged in state. And all of this is done in 1 or 2 lines of code to maintain the simplicity and flexibility Leaf auth has always given.

To get started with session support, just set the `USE_SESSION` setting to true.

```php
$auth->config("USE_SESSION", true);
```

A much simpler way would be to simply call the `useSession` method.

```php
$auth->useSession();
```

## Session methods <sup class="new-tag-1">New in v2.4.1</sup>

Enabling session support allows you to use some special methods and behaviours which are not available with the regular JWT authentication.

### guard <sup class="new-tag-1">New in v2.4.1</sup>

The guard method works sort of like authentication middleware. It takes in a single param, an array holding the authentication state or the type of guard to load up.

```php
$auth->guard(["hasAuth" => true]);

// or

$auth->guard("auth");

// guest route redirects to home
// route if you're logged in
$auth->guard("guest");
```

### saveToSession <sup class="new-tag-1">New in v2.4.1</sup>

This method is used to save a variable to the auth session.

```php
$auth->saveToSession("rememberLogin", false);

// You can add multiple vars
$auth->saveToSession([
  "rememberLogin" => false,
  "sessionActivity" => "login"
]);
```

### sessionLength <sup class="new-tag-1">New in v2.4.1</sup>

With sessionLength, you can get how long a user has been logged in. You can save the session time logs to your database in order to track users' login logs. The available logs are `SESSION_STARTED_AT` and `SESSION_LAST_ACTIVITY` which are automatically tracked by Leaf.

```php
// LoginsDB is a user defined method to save a login log

// ...
LoginsDB::params(
  "logged_in_at",
  date("D, d M Y H:i:s", $auth->sessionLength()),
);

LoginsDB::save();
```

### sessionActive <sup class="new-tag-1">New in v2.4.1</sup>

sessionActive allows you to get how much time has passed since the last session activity.

```php
$userLastSeen = $auth->sessionActive();
```

### refresh <sup class="new-tag-1">New in v2.4.1</sup>

As the name implies, you can refresh the session with this method. Refreshing sort of restarts the session, but you can keep the user's old session data if you wish to.

```php
if ($newAccountAdded) {
  // will delete old session data
  $auth->refresh();
} else {
  // will keep session data
  $auth->refresh(false);
}
```

### session <sup class="new-tag-1">New in v2.4.1</sup>

session checks whether a user session is ongoing by looking for keys specific to Leaf session auth so it doesn't confuse a Leaf auth session with user defined sessions. Returns true if a session is found and false if there's no session found.

```php
if ($auth->session()) {
  return "logged in";
} else {
  return "guest mode";
}
```

### endSession <sup class="new-tag-1">New in v2.4.1</sup>

Of course we'll need a method to logout/end our session. This is just the method for that.

```php
$auth->endSession();
```

**login, register and the other methods used in auth now integrate with auth when they're used. So login will start a session instead of returning a JWT.**

Read the section below to learn more about the main authentication methods and what session support that has been added.

## Authentication methods

### login

Login is used to create a simple, secure user login. It takes in a table to search for users(so it's no longer limited to the users table) and a set of parameters for the login.

```php
$user = $auth->login("users", [
  "username" => "mychi.darko",
  "password" => md5("test")
]);
```

If the user is successfully found, the user data is returned, if not, `null` is returned. You can get any error by calling the `errors` method.

```php
$user = $auth->login("users", [
  "username" => "mychi.darko",
  "password" => md5("test")
]); // returns null if failed

if (!$user) {
  $response->throwErr($auth->errors());
}
```

example success response:
**Note that the password and id fields are removed**. In v2.4-beta, you can control whether fields should be hidden from the returned value in the Auth settings.

```php
[
  "user" => [
    "username" => "mychi.darko",
    "email" => "mickdd22@gmail.com",
    "created_at" => "2019-09-20 13:47:48"
  ],
  "token" => "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE1NzYxMzUzMjgsImlzcyI6ImxvY2FsaG9zdCIsImV4cCI6MTU3NjEzNjIyOCwidXNlcklkIjoxfQ.7FODXGGJKioGQVX4ic0DJLoMIQTVUlsd4zFAJA4DAkg"
]
```

#### session support <sup class="new-tag-1">New in v2.4.1</sup>

Login received session support which allows login to create a session instead of returning aa JWT as done by default. To get started with session, just set the `USE_SESSION` setting or call the `useSession` method.

```php
$auth->useSession();

$auth->login("users", [
  "username" => $username,
  "password" => $password
]);
```

When the login succeeds, you'll be redirected to GUARD_HOME. You can configure the GUARD_HOME route to match the needs of your app.

In case there's something wrong and Auth can't sign the user in, it returns a falsy value.

```php
$user = $auth->login("users", [
  "username" => $username,
  "password" => $password
]);

if (!$user) {
  // you can pass the auth errors into a view
  return $blade->render("pages.auth.login", [
    "errors" => $auth->errors(),
    "username" => $username,
    "password" => $password,
  ]);
}
```

#### Password Encoding

From v2.4-beta onwards, password encoding will no longer be available on the login method, you have to configure it among the Auth settings instead.

`login` has a 3rd parameter which is an array of validation rules for login data.

```php
// validation rules
$rules = ["username" => "ValidUsername"];

$user = $auth->login("users", $loginData, $rules);
```

To get any errors, you need to call the `errors` method

```php
if (!$user) {
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
  $auth->register("users", $app->request()->body(), ["username", "email"]);
});
```

So, we pass in the entire request body, which contains the username, email and password. Simple right?

The password encode option here has also been removed. Use the auth config above instead. The final parameter is now the validate param which is an array of rules to test the params.

```php
$app->post("/register", function() use($app) {
  $auth->register("users", $app->request()->body(), ["username", "email"], ["email" => "email"]);
});
```

#### register session support <sup class="new-tag-1">New in v2.4.1</sup>

Just as with login, register now integrates with session. To turn this feature on, just set the `USE_SESSION` setting or call the `useSession` method.

```php
$auth->useSession();

$auth->register("users", $credentials, [
  "username", "email"
]);
```

After a successful registration, you can redirect to GUARD_HOME or rather GUARD_LOGIN if you want the user to login after registration.

```php
// set your login route...default is /auth/login
$auth->config("GUARD_LOGIN", "/login");

// Redirect to login after auth
$auth->config("SESSION_ON_REGISTER", false);

// Login automatically after registration
$auth->config("SESSION_ON_REGISTER", true);
```

In case there's something wrong and Auth can't register the user, it returns a falsy value.

```php
$user = $auth->register("users", $credentials, [
  "username", "email"
]);

if (!$user) {
  // you can pass the auth errors into a view
  return $blade->render("pages.auth.register", [
    "errors" => $auth->errors(),
    "username" => $username,
    "email" => $email,
    "password" => $password,
  ]);
}
```

<hr>

### update

There's a login method, a register method, so why not a user update method? This method takes the stress out of updating a user's information. Update takes in 5 parameters:

- The table to look for users
- The data to update
- Credentials to find user by
- Unique values (optional)
- Validation array (optional)

```php
// data to update
$data = $request->get(["username", "email"]);

// credentials to find user by
$where = ["id" => 2];

// unique data
$uniques = ["username", "email"];

// validation
$validation = ["username" => "ValidUsername", "email" => "email"];

$user = $auth->update("users", $data, $where, $uniques, $validation);
```

**Something little:** Uniques in `update` work a bit different from `register`, in `update`, Leaf tries to find another user which isn't the current user that has the same credentials. So if there's no other user with that same param value, the unique test passes. In short, **the current user is excluded from the users to check for same credentials**

#### update session support <sup class="new-tag-1">New in v2.4.1</sup>

Update also reeived session support. When a user is updated, the user is updated in the session and the updated user is also returned.

```php
$user = $this->auth->update("users", $data, $where, $uniques);
```

<hr>

### user

<p class="alert -warning">
  This was previously <b>currentUser</b>
</p>

When tokens are added inside requests, you generally have to decode the token and query your database with the id returned to get the current user. Although Leaf Auth makes it really simple, it can get even simpler; by calling a single method. It takes in one parameter, the table to look for users.

```php
$user = $auth->user("users");
return $user["name"];
```

In v2.4 beta, the table is set to `users` by default. So you can simply do this:

```php
$user = $auth->user();
```

We can catch any errors that occur, from fetching the user, working with the token...

```php
$user = $auth->user() ?? $request->throwErr($auth->errors());
```

`user` also takes in a second parameter, which is an array of items to hide from the user array.

```php
$user = $auth->user("users", ["id", "password"]);
```

<hr>

### id

<p class="alert -warning">
  This was previously <b>useToken</b>
</p>

This is a method that decodes a token and returns the `user_id` field encoded in it.

```php
$user_id = $auth->id();
```

<hr>

### [Leaf Authentication Methods](leaf/v/2.4-beta/core/authentication)

Leaf Auth now uses the `Leaf\Helpers\Authentication` package to provide solutions for token authentication. This provides a simple way to work with manual authentication and tokens. All methods here are now available in `Leaf\Auth`.

```php
$payload = $auth->validate($token);
```

Read [authentication](leaf/v/2.4-beta/core/authentication) for more info

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

<a href="#/v/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/v/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/v/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
