<!-- markdownlint-disable no-inline-html -->
# 🚇 Sub-routing

Use `$app->mount($baseroute, $fn)` or `$app->group` to mount a collection of routes onto a subroute pattern. The subroute pattern is prefixed onto all following routes defined in the scope. e.g. Mounting a callback $fn onto `/movies` will prefix `/movies` onto all following routes.

```php
$app->mount('/movies', function() use ($app) {
    // will result in '/movies/'
    $app->get('/', function() {
        echo 'movies overview';
    });

    // will result in '/movies/id'
    $app->get('/(\d+)', function($id) {
        echo 'movie id ' . htmlentities($id);
    });
});
```

Nesting of subroutes is possible, just define a second `$app->mount()` in the callback function that's already contained within a preceding `$app->mount()`. Also, Note that nested subroutes currently don't support dynamic url patterns, so, you can only do something like this.

```php
$app->group('/user', function() use ($app) {
    $app->get('/', function() use($app) {
        echo $app->response->renderMarkup('no user id');
    });

    $app->get('/(\d+)', function($id) use($app) {
        echo $app->response->renderMarkup("user $id");
    });

    $app->mount('/settings', function() use ($app) {
        $app->get('/privacy', function() use($app) {
            echo $app->response->renderMarkup('Privacy Settings');
        });

        $app->get('/notification', function() use($app) {
            echo $app->response->renderMarkup("Notification Settings");
        });
    });
});
```

## Group Namespaces <sup class="new-tag-1">New</sup>

You can now select namespaces for individual groups of routes. Usually, a namespace is given to all your routes, however, a group may need a different namespace for it's controllers and that is what Leaf gives you.

```php
$app->setNamespace("App\Controllers");

$app->group("/user", ["namespace" => "Lib\Controllers", function() use($app) {
    // controller here will be Lib\Controllers\FormsController
    $app->get("/form", "FormsController@index");
}]);

// controller here will be App\Controllers\FormsController
$app->get("/form", "FormsController@index");
```

<br>
<hr>

## Next Steps

- [Dynamic Routing](leaf/v/2.5.0/routing/dynamic)
- [Error Handling](leaf/v/2.5.0/routing/errors)
- [Middleware](leaf/v/2.5.0/routing/middleware)
- [Using Controllers](leaf/v/2.5.0/routing/controller)

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
