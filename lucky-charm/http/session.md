<!-- markdownlint-disable no-inline-html -->
# 😷 Leaf Sessions

Leaf offers simple session management to help you quickly build your apps and APIs.

**Note:** In version 2, `\Leaf\Core\Http\Session` has been shortened to `\Leaf\Http\Session`.

## Using Session

```php
$app = new Leaf\App;
$session = new Leaf\Http\Session();

$app->get("/text", function() use($session) {
  $session->set("name", "Michael Darko");
});
```

### Initialising the Session object

With this method, you manually initialise the Session object, and then pass it into your route. Note that in version 2, `\Leaf\Core\Http\Session` has been shortened to `\Leaf\Http\Session`.

```php
$app = new Leaf\App;
$session = new Leaf\Http\Session;

$app->post("/login", function() use($session) {
  // ...
  $session->set("username", $username);
});
```

<hr>

## Starting a new session

A new session is started or an old one continued when you instanciate the `Leaf\Http\Session`.

```php
// new session not started
$session = new Leaf\Http\Session(false);

// new session/continue session
$session = new Leaf\Http\Session;

// new session/continue session
$session = new Leaf\Http\Session(true);
```

Since we want to avoid sessions conflicting, Lucky Charm allows you to choose whether you want to start a new session on init. This also allows smooth integration with native PHP sessions, so you can always switch to Leaf sessions when you're ready.

<hr>

## Leaf Session Methods

From this point on you'll be able to use everything Leaf Sessions have to offer. Let's look at the session methods.

### set

set simply sets new native session variables for your app.

```php
$session->set("username", $username);
```

#### Setting multiple values

In v2.0, `set` can take in an array if you wish to set multiple values or just want to use one.

```php
$session->set(["username" => $username, "mobile_number" => $mobile_number]);
```

<hr>

### get

get is a simple method that returns a session value. It takes in one parameter: the name of the param passed into the app through the session It works just like how `$_SESSION['key']` does.

```php
$username = $session->get("username");
```

#### Multiple Get <sup class="new-tag-1">New in Lucky Charm🍀</sup>

In Lucky Charm, you can return many fields at once from the session:

```php
$user = $session->get(["username", "email"]);
```

#### Security Fixes <sup class="new-tag-1">New in Lucky Charm🍀</sup>

`set()` has also received a bunch of security fixes which prevent maliscious scripts from being passed into your application. In Lucky Charm, you can choose to turn this feature off, maybe for html values:

```php
// turn off sanitize
$html = $session->get("blog", false);
```

<hr>

## retrieve

retrieve returns the requested value and removes it from the session, just like calling `get` first and then `unset` for the same key.

It takes in two parameters:

- the name of the param you want to get It works just like how `$_SESSION['key']` does

- The default value to use if it doesn't exist.

```php
$username = $session>retrieve("username");
```

<hr>

### body

body returns the key => value pairs of all the session data including any CSRF data as an associative array.

```php
$body = $session->body();
```

<hr>

### unset

**NOTE: In v2, `remove` has been renamed to `unset`**

`unset` simply deletes a session variable. You can also delete multiple values at once.

```php
// single value
$session->unset('email');
// multiple values
$session->unset(['name', 'email']);
```

<hr>

### reset

`reset` simply re-initialises a session.

```php
$app->post('/session/reset', function() use($session) {
 $session->reset();
});
```

<hr>

### id

`id` sets and/or returns the current session id. It takes in an **optional** parameter: the ID to overwrite the session id.

```php
$id = $session->id();
```

So if the session id is not set, this will generate and return a new session id. However, if the session id is already set, it will just return it.

You can also set your own session id with this syntax below. It will be returned as well, so you can keep it in a variable.

```php
$id = $session->id("new session id");
```

<hr>

### regenerate

regenerate simply generates a new session id. It takes in a boolean parameter which indicates whether to delete all session data or not(has a default of false)

```php
$session->regenerate();
$session->regenerate(false);
$session->regenerate(true); // will clear all session data
```

### destroy

Just as you cann start a session, you can also end a session with `destroy`.

```php
$session->destroy();
```

### encode <sup class="new-tag-1">New in Lucky Charm🍀</sup>

Lucky Charm comes with the encode feature which allows you to encode the current session data as a string.

```php
$sessionString = $session->encode();
```

### decode <sup class="new-tag-1">New in Lucky Charm🍀</sup>

You can also decode a serialized session using the `decode` method. It takes in the string to decode.

```php
$phpSession = $session->decode($sessionString);
```

## Error Handling <sup class="new-tag-1">New in Lucky Charm🍀</sup>

In previous versions of Leaf, sessions would always throw errors directly which made them not very suitable for web app development, however, lucky charm fixes that problem. If any of the above methods fail an operation, `false` is returned and an error is left in the `Leaf\Http\Session` local state. This error or errors can be returned by calling the `errors` method.

```php
$user = $session->get("user");
if (!$user) $response->throwErr($session->errors());
```

As you can see, you'd manually need to throw errors, this gives you more flexibility in web apps, so instead of throwing session errors, you might do something like this:

```php
<?php
// ...
foreach ($session->errors() as $error => $value) {
  echo "<b>{$value}</b>";
}
```

<br>
<hr>

<a href="#/lucky-charm/http/response" style="margin: 0px">Response</a>
<a href="#/lucky-charm/http/request" style="margin: 0px; 10px;">Request</a>
<a href="#/lucky-charm/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/lucky-charm/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
