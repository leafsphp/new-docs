# Cookies 

The Leaf application provides helper methods to send cookies with the HTTP response.

## Set Cookie

This example demonstrates how to use the Leaf application’s `setCookie()` method to create an HTTP cookie to be sent with the HTTP response:

```php
$leaf->setCookie('foo', 'bar', '2 days');
```

This creates an HTTP cookie with the name `“foo”` and value `“bar”` that expires two days from now. You may also provide additional cookie properties, including its path, domain, secure, and httponly settings. The Leaf application’s setCookie() method uses the same signature as PHP’s native setCookie() function.

```php
$leaf->setCookie(
    $name,
    $value,
    $expiresAt,
    $path,
    $domain,
    $secure,
    $httponly
);
```

<hr>

## Set Encrypted Cookie

You can tell Leaf to encrypt the response cookies by setting the app’s cookies.encrypt setting to true. When this setting is true, Leaf will encrypt the response cookies automatically before they are returned to the HTTP client.

Here are the available Leaf app settings used for cookie encryption:

```php
$leaf = new \Leaf\App([
    'cookies.encrypt' => true,
    'cookies.secret_key' => 'my_secret_key',
    'cookies.cipher' => MCRYPT_RIJNDAEL_256,
    'cookies.cipher_mode' => MCRYPT_MODE_CBC
]);
```

<hr>

## Delete Cookie

You can delete a cookie using the Leaf application’s `deleteCookie()` method. This will remove the cookie from the HTTP client before the next HTTP request. This method accepts the same signature as the Leaf application’s `setCookie()` instance method, without the `$expires` argument. Only the first argument is required.

```php
$leaf->deleteCookie('foo');
```

If you need to also specify the path and domain:

```php
$leaf->deleteCookie('foo', '/', 'foo.com');
```
You may also further specify the secure and httponly properties:

```php
$leaf->deleteCookie('foo', '/', 'foo.com', true, true);
```

<hr>

## [Session Cookies](2.1http/session?id=sesison-cookies-span-stylebackground-rgb11-200-70-color-white-padding-3px-7px-font-size-14pxnew-in-v2)

<br>
<hr>

<a href="#/leaf/v/2.1-apha/http/response" style="margin: 0px">Response</a>
<a href="#/leaf/v/2.1-apha/http/request" style="margin: 0px; 10px;">Request</a>
<a href="#/leaf/v/2.1-apha/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/leaf/v/2.1-apha/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
