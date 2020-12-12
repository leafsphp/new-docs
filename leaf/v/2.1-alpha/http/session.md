# Leaf Sessions

Leaf offers simple session management to help you quickly build your apps and APIs.

**Note:** In version 2, `\Leaf\Core\Http\Session` has been shortened to `\Leaf\Http\Session`.

## Using Session

```php
$leaf = new Leaf\App();
$session = new Leaf\Http\Session();

$leaf->get("/text", function() use($session) {
	$session->set("name", "Michael Darko");
});
```

### Initialising the Session object

With this method, you manually initialise the Session object, and then pass it into your route. Note that in version 2, `\Leaf\Http\Session` has been shortened to `\Leaf\Http\Session`.

```php
$leaf = new Leaf\App();
$session = new Leaf\Http\Session();

$leaf->post("/login", function() use($session) {
	...
	$session->set("username", $username);
});
```

<hr>

## Starting a new session

A new session is started or an old one continued when you instanciate the `Leaf\Session`

```php
// more direct method
$session = new Leaf\Http\Session;
```

This line of code checks for an active session....if none is found, it creates a new session, if one is running, it just instanciates the Session object to be used in Leaf

<hr>

## set()

set() simply sets new native session variables for your app.

```php
$session->set("username", $username);
```

#### Setting multiple values

In v2.0, `set` can take in an array if you wish to set multiple values or just want to use one.
```php
$session->set(["username" => $username, "mobile_number" => $mobile_number]);
```

#### Security Fixes

`set()` has also received a bunch of security fixes which prevent maliscious scripts from being passed into your application.

<hr>

## get()

get is a simple method that returns a session value. It takes in one parameter: the name of the param passed into the app through the session It works just like how `$_SESSION['key']` does
```php
$username = $session>get("username");
```

<hr>

## retrieve()

retrieve returns the requested value and removes it from the session, just like calling `get` first and then `unset` for the same key.

It takes in two parameters:

- the name of the param you want to get It works just like how `$_SESSION['key']` does

- The default value to use if it doesn't exist.

```php
$username = $session>retrieve("username");
```

<hr>

## getBody()

getBody() returns the key => value pairs of all the session data including any CSRF data as an associative array.

```php
$body = $session->getBody();
```

<hr>

## unset()

**NOTE: In v2, `remove` has been renamed to `unset`**

`unset()` simply deletes a session variable.

```php
$session->unset('name');
```

### Removing multiple values

In v2.0, `unset` can also take in an array if you wish to unset multiple values or just want to use one.

```php
$session->unset(["username", "mobile_number"]);
```

<hr>

## reset()

`reset()` simply re-initialises a session.

```php
$leaf->post('/session/reset', function() use($session) {
  	$session->reset();
});
```

<hr>

## id()

`id()` sets and/or returns the current session id. It takes in an **optional** parameter: the ID to overwrite the session id.

```php
$id = $session->id();
```

So if the session id is not set, this will generate and return a new session id. However, if the session id is already set, it will just return it.

You can also set your own session id with this syntax below. It will be returned as well, so you can keep it in a variable.

```php
$id = $session->id("new session id");
```

<hr>

## regenerate()
regenerate() simply generates a new session id. It takes in a boolean parameter which indicates whether to delete all session data or not(has a default of false)

```php
$session->regenerate(false);
$session->regenerate(true); // will clear all session data
```

<hr>

## Sesison Cookies 
You may also use the `\Leaf\Middleware\SessionCookie` middleware to persist session data in encrypted, hashed HTTP cookies. To enable the session cookie middleware, add the `\Leaf\Middleware\SessionCookie` middleware to your Leaf application:

```php
$leaf->add(new \Leaf\Middleware\SessionCookie(array(
    'expires' => '20 minutes',
    'path' => '/',
    'domain' => null,
    'secure' => false,
    'httponly' => false,
    'name' => 'leaf_session',
    'secret' => 'CHANGE_ME',
    'cipher' => MCRYPT_RIJNDAEL_256,
    'cipher_mode' => MCRYPT_MODE_CBC
)));
```

The second argument is optional; it is shown here so you can see the default middleware settings. The session cookie middleware will work seamlessly with the `$_SESSION` superglobal so you can easily migrate to this session storage middleware with zero changes to your application code.

If you use the session cookie middleware, you DO NOT need to start a native PHP session. The `$_SESSION` superglobal will still be available, and it will be persisted into an HTTP cookie via the middleware layer rather than with PHP’s native session management.

Remember, HTTP cookies are inherently limited to only 4 kilobytes of data. If your encrypted session data will exceed this length, you should instead rely on PHP’s native sessions or an alternate session store.

***NOTE***: **Client-side storage of session data is not recommended if you are dealing with sensitive information, even when using Leaf's encrypted session cookie middleware. If you need to store sensitive information, you should encrypt and store the session information on your server.**

<br>
<hr>

<a href="#/leaf/v/2.1-apha/http/response" style="margin: 0px">Response</a>
<a href="#/leaf/v/2.1-apha/http/request" style="margin: 0px; 10px;">Request</a>
<a href="#/leaf/v/2.1-apha/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/leaf/v/2.1-apha/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>