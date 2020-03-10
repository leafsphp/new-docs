# Leaf Sessions
Leaf offers simple session management to help you quickly build your apps and APIs.

**Note:** In version 2, `\Leaf\Core\Http\Session` has been shortened to `\Leaf\Http\Session`. Also the session object is available on `$leaf->session`.

## Using Session
### Session on the Leaf Instance <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span></sup>
Since Session is already bound to the Leaf instance, you can do this:
```js
$leaf = new Leaf\App();

$leaf->get("/text", function() use($leaf) {
	$leaf->session->set("name", "Michael Darko");
});
```
Although we've added this, we don't want to force you to do stuff in only one way, so you can still use the `v1.x` method.

### Initialising the Session object
With this method, you manually initialise the Session object, and then pass it into your route. Note that in version 2, `\Leaf\Core\Http\Session` has been shortened to `\Leaf\Http\Session`.
```js
$leaf = new Leaf\App();
$session = new Leaf\Http\Session();

$leaf->post("/login", function() use($session) {
	...
	$session->set("username", $username);
});
```

<hr>

## Starting a new session
Starting a new session with leaf is actually very simple😅..

```js
// new in v2
$leaf->session;

// more direct method
new Leaf\Http\Session;
```
This line of code checks for an active session....if none is found, it creates a new session, if one is running, it just instanciates the Session object to be used in Leaf

<hr>

## set()
set() simply sets new native session variables for your app.

```js
$session->set("username", $username);
```

#### Setting multiple values <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 11px;">New in v2</span></sup>
In v2.0, `set` can take in an array if you wish to set multiple values or just want to use one.
```js
$leaf->session->set(["username" => $username, "mobile_number" => $mobile_number]);
```

#### Security Fixes <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 11px;">New in v2</span></sup>
`set()` has also received a bunch of security fixes which prevent maliscious scripts from being passed into your application.

<hr>

## get()
get is a simple method that returns a session value. It takes in one parameter: the name of the param passed into the app through the session It works just like how `$_SESSION['key']` does
```js
$username = $leaf-->session>get("username");
```

<hr>

## getBody()
getBody() returns the key => value pairs of all the session data including any CSRF data as an associative array.

```js
$bosy = $leaf->session->getBody();
```

<hr>

## unset()
**NOTE: In v2, `remove` has been renamed to `unset`**

`unset()` simply deletes a session variable.

```js
$leaf->session->unset('name');
```

### Removing multiple values <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 11px;">New in v2</span></sup>
In v2.0, `unset` can also take in an array if you wish to unset multiple values or just want to use one.
```js
$leaf->session->unset(["username", "mobile_number"]);
```

<hr>

## reset()
`reset()` simply re-initialises a session.
```js
$leaf->post('/session/reset', function() use($session) {
  	$session->reset();
});
```

<hr>

## id()
`id()` sets and/or returns the current session id. It takes in an **optional** parameter: the ID to overwrite the session id.

```js
$id = $leaf->session->id();
```
So if the session id is not set, this will generate and return a new session id. However, if the session id is already set, it will just return it.


You can also set your own session id with this syntax below. It will be returned as well, so you can keep it in a variable.
```js
$id = $leaf->session->id("new session id");
```

<hr>

## regenerate()
regenerate() simply generates a new session id. It takes in a boolean parameter which indicates whether to delete all session data or not(has a default of false)

```js
$leaf->session->regenerate(false);
$leaf->session->regenerate(true); // will clear all session data
```

<hr>

## Sesison Cookies <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span></sup>
You may also use the `\Leaf\Middleware\SessionCookie` middleware to persist session data in encrypted, hashed HTTP cookies. To enable the session cookie middleware, add the `\Leaf\Middleware\SessionCookie` middleware to your Leaf application:

```js
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

<a href="#/2.0/http/response" style="margin: 0px">Response</a>
<a href="#/2.0/http/request" style="margin: 0px; 10px;">Request</a>
<a href="#/2.0/database/intro" style="margin: 0px 10px;">Environment</a>
<a href="#/2.0/database/intro" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>