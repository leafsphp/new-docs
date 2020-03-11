# Blade Templating <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span></sup>

This is Leaf's implementation of Laravel's blade templating engine. It is an independent package, but has been added and bound to Leaf Core. So just like other packages, you don't need to instanciate it if you don't want to.

```js
// on the leaf object
$leaf->blade;
```

```js
// initialising the package
$blade = new Leaf\Blade();
```

## Usage
To further understand blade, you can view the official documentation http://laravel.com/docs/5.8/blade.

Leaf Blade only supports directory configurations, which can be passed as params on initialisation.
```js
use Leaf\Blade;

// Blade("template dir", "cache dir");
$blade = new Blade('app/views', 'app/views/cache'); 
```

Not to worry, you can configure blade at a later time after initialisation.

```js
$blade = new Leaf\Blade;

// somewhere, maybe in a different file
$blade->configure("app/views", "app/views/cache");
```

Since Blade is also bound directly to the Leaf object, you can directly do this

```js
$leaf->blade->configure("app/views", "app/views/cache");
```

Now that this is done, we can render our blade template. This is done with `make`.

```js
// don't forget to chain the render method
echo $blade->make('index', ['name' => 'Michael Darko'])->render(); // index.blade.php
```

Alternatively you can use the shorthand method render:

```js
echo $blade->render('index', ['name' => 'Michael Darko']);
```

We can have this as our template index.blade.php

```html
<!Doctype html>
<html>
    <head>
        <title>{{ $name }}</title>
    </head>
    <body>
        <div class="container">{{ $name }}</div>
    </body>
</html>
```

You can also extend Blade using the `directive()` function:

```js
$blade->directive('datetime', function ($expression) {
    return "<?php echo with({$expression})->format('F d, Y g:i a'); ?>";
});
```

Which allows you to use the following in your blade template:

```html
Current date: @datetime($date)
```

The Blade instances passes all methods to the internal view factory. So methods such as exists, file, share, composer and creator are available as well. Check out the [original documentation](http://laravel.com/docs/5.8/blade) for more information.

<br>
<hr>

<a href="#/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>