# App Settings

## mode

This is an identifier for the application’s current mode of operation. The mode does not affect a Leaf application’s internal functionality. Instead, the mode is only for you to optionally invoke your own code for a given mode with the `configMode()` application method.

The application mode is declared during instantiation, either as an environment variable or as an argument to the Leaf application constructor. It cannot be changed afterward. The mode may be anything you want — “development”, “test”, and “production” are typical, but you are free to use anything you want (e.g. “foo”).

```php
$app = new \Leaf\App([
    'mode' => 'development'
]);
```

**Mode Down.**

You can now set the mode to `down`, and this will place the app in maintainance mode. In maintainance mode, no requests will be handled, and the maintainace page will be displayed. You can set your own template or reponse in place of the default app down page.

```php
$app = new \Leaf\App([
    'mode' => 'down'
]);

$app->setDown(function() use($app) {
    $app->response()->page("./templates/down.html");
});
```

<hr>

## debug

If debugging is enabled, Leaf will use its built-in error handler to display diagnostic information for uncaught Exceptions. If debugging is disabled, Leaf will instead invoke your custom error handler, passing it the otherwise uncaught Exception as its first and only argument.

```php
$app = new \Leaf\App([
  'debug' => true
]);
```

<hr>

## log.writer

Use a custom log writer to direct logged messages to the appropriate output destination. By default, Leaf’s logger will write logged messages to `STDERR`. If you use a custom log writer, it must implement this interface:

```php
public write(mixed $message, int $level);
```

The `write()` method is responsible for sending the logged message (not necessarily a string) to the appropriate output destination (e.g. a text file, a database, or a remote web service).

To specify a custom log writer after instantiation you must access Leaf’s logger directly and use its `setWriter()` method:

```php
// During instantiation
$app = new \Leaf\App([
  'log.writer' => new \My\LogWriter()
]);

// After instantiation
$log = $app->getLog();
$log->setWriter(new \My\LogWriter());
```

<hr>

## log.level

Leaf has these log levels:

- \Leaf\Log::EMERGENCY
- \Leaf\Log::ALERT
- \Leaf\Log::CRITICAL
- \Leaf\Log::ERROR
- \Leaf\Log::WARN
- \Leaf\Log::NOTICE
- \Leaf\Log::INFO
- \Leaf\Log::DEBUG

The `log.level` application setting determines which logged messages will be honored and which will be ignored. For example, if the `log.level` setting is `\Leaf\Log::INFO`, debug messages will be ignored while info, warn, error, and fatal messages will be logged.

To change this setting after instantiation you must access Leaf’s logger directly and use its `setLevel()` method.

```php
// During instantiation
$app = new \Leaf\App([
    'log.level' => \Leaf\Log::DEBUG
]);

// After instantiation
$log = $app->getLog();
$log->setLevel(\Leaf\Log::WARN);
```

<hr>

## log.enabled

This enables or disables Leaf’s logger. To change this setting after instantiation you need to access Leaf’s logger directly and use its `setEnabled()` method.

```php
// During instantiation
$app = new \Leaf\App([
    'log.enabled' => true
]);

// After instantiation
$log = $app->getLog();
$log->setEnabled(true);
```

<hr>

## templates.path

The relative or absolute path to the filesystem directory that contains your Leaf application’s template files. This path is referenced by the Leaf application’s View to fetch and render templates.

To change this setting after instantiation you need to access Leaf’s view directly and use its `setTemplatesDirectory()` method.

```php
// During instantiation
$app = new \Leaf\App([
    'templates.path' => './templates'
]);

// After instantiation
$view = $app->view();
$view->setTemplatesDirectory('./templates');
```

<hr>

## view

The View class or instance used by the Leaf application. To change this setting after instantiation you need to use the Leaf application’s `view()` method.

```php
// During instantiation
$app = new \Leaf\App([
    'view' => new \My\View()
]);

// After instantiation
$app->view(new \My\View());
```

<hr>

## cookies.encrypt

Determines if the Leaf app should encrypt its HTTP cookies.

```php
$app = new \Leaf\App([
    'cookies.encrypt' => true
]);
```

<hr>

## cookies.lifetime

Determines the lifetime of HTTP cookies created by the Leaf application. If this is an integer, it must be a valid UNIX timestamp at which the cookie expires. If this is a string, it is parsed by the strtotime() function to extrapolate a valid UNIX timestamp at which the cookie expires.

```php
$app = new \Leaf\App([
    'cookies.lifetime' => '20 minutes'
]);

// After instantiation
$app->config('cookies.lifetime', '20 minutes');
```

<hr>

## cookies.path

Determines the default HTTP cookie path if none is specified when invoking the Leaf application’s `setCookie()` or `setEncryptedCookie()` methods.

```php
$app = new \Leaf\App([
  'cookies.path' => '/'
));

// After instantiation
$app->config('cookies.path', '/');
```

<hr>

## cookies.domain

Determines the default HTTP cookie domain if none specified when invoking the Leaf application’s `setCookie()` or `setEncryptedCookie()` methods.

```php
$app = new \Leaf\App([
  'cookies.domain' => 'domain.com'
));

// After instantiation
$app->config('cookies.domain', 'domain.com');
```

<hr>

## cookies.secure

Determines whether or not cookies are delivered only via HTTPS. You may override this setting when invoking the Leaf application’s `setCookie()` or `setEncryptedCookie()` methods

```php
$app = new \Leaf\App([
  'cookies.secure' => false
));

// After instantiation
$app->config('cookies.secure', false);
```

<hr>

## cookies.httponly

Determines whether cookies should be accessible through client side scripts (false = accessible). You may override this setting when invoking the Leaf application’s `setCookie()` or `setEncryptedCookie()` methods.

```php
$app = new \Leaf\App([
  'cookies.httponly' => false
));

// After instantiation
$app->config('cookies.httponly', false);
```

<hr>

## cookies.secret_key

The secret key used for cookie encryption. You should change this setting if you use encrypted HTTP cookies in your Leaf application.

```php
$app = new \Leaf\App([
  'cookies.secret_key' => 'secret'
));

// After instantiation
$app->config('cookies.secret_key', 'secret');
```

<hr>

## cookies.cipher

The mcrypt cipher used for HTTP cookie encryption. [See available ciphers.](http://php.net/manual/en/mcrypt.ciphers.php)

```php
$app = new \Leaf\App([
  'cookies.cipher' => MCRYPT_RIJNDAEL_256
));

// After instantiation
$app->config('cookies.cipher', MCRYPT_RIJNDAEL_256);
```

<hr>

## cookies.cipher_mode

The mcrypt cipher used for HTTP cookie encryption. [See available ciphers.](http://php.net/manual/en/mcrypt.ciphers.php)

```php
$app = new \Leaf\App([
  'cookies.cipher_mode' => MCRYPT_MODE_CBC
));

// After instantiation
$app->config('cookies.cipher_mode', MCRYPT_MODE_CBC);
```

<hr>

## http.version

By default, Leaf returns an HTTP/1.1 response to the client. Use this setting if you need to return an HTTP/1.0 response. This is useful if you use PHPFog or an nginx server configuration where you communicate with backend proxies rather than directly with the HTTP client.

```php
$app = new \Leaf\App([
  'http.version' => '1.1'
));

// After instantiation
$app->config('http.version', '1.1');
```

<hr>

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
