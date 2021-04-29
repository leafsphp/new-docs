<!-- markdownlint-disable no-inline-html -->
# Changes in Leaf router

Leaf router has seen huge improvements, usability upgrades, bug fixes and of course new features. This page was created to give you a fair idea of what these changes are and how to use them.

## New Features

### Route options

This is the biggest change Leaf router has seen over the period of a year. Route options simply allow you to configure the way groups and individual routes by passing in additional parameters. In actual sense, all new features were generated as a result of this single feature. Let's see how it works.

Leaf route handlers are usually callable functions like this:

```php
$app->get("/home", function() {
  echo "User Home";
});
```

Or sometimes controllers, like this:

```php
$app->get("/home", "HomeController@index");
```

This means there was no space to chain additional items to the route, this is solved by route options.

```php
$app->get("/home", ["name" => "home", function() {
    echo "User Home";
}]);
```

When an array is passed into a leaf route as the handler, leaf will take all `key => value` as options for that route, the first non key-value `function` or `controller` in the array is taken as the handler.

```php
$app->get("/form", ["name" => "userForm", "FormsController@index"]);
```

As mentioned before, this feature is also available on groups:

```php
$app->group("/user", ["namespace" => "\\", function() use($app) {
    // ...
}]);
```

**This doesn't mean that you should always pass in an array, if you don't need the other options, you can pass in your function or controller directly as you've always done.**

### Single route options

These are the options available on individual routes.

#### namespace

This allows you to change the default controller namespace for a given route. Leaf router allows you to set a namespace to chain to all your controllers, however, some controllers may come from a third party library and may have a different namespace. This is when you use this option.

```php
$app->get("/form", ["namespace" => "\\", "FormsController@index"]);
```

#### middleware

This is a new way to quickly setup middleware for a particular route. Leaf has the before method which allows you to set a route specific middleware, but that means defining the same route twice, not to mention, you may mistake the middleware for the main route as they have the same syntax. This problem is solved by the middleware option. **If your prefer using `before`, you can always do so.**

```php
// you can define it in a different file
$homeMiddleware = function () {
    echo "Home middleware";
};

$app->get("/home", ["middleware" => $homeMiddleware, function() {
    echo "User Home";
}]);
```

#### name

You can give route names which you can call them with instead of using the path (Inspired by vue-router).

```php
$app->get("/home", ["name" => "profile", function() {
    echo "User Home";
}]);
```

### Router push

This is simply redirecting to a route and can be done using `push`. `push` also allows you to reference the route by it's name instead of it's path.

```php
$app->router()->push("/profile");
```

When an array is passed into push, Leaf will search for a route name matching the string in the array and redirect to that route:

```php
// home was defined above
$app->router()->push(["home"]);
```

### Group Namespaces

As seen before, you can now select namespaces for individual groups of routes. Usually, a namespace is given to all your routes, however, a group may need a different namespace for it's controllers and that is what Leaf gives you.

```php
$app->setNamespace("App\Controllers");

$app->group("/user", ["namespace" => "Lib\Controllers", function() use($app) {
    // controller here will be Lib\Controllers\FormsController
    $app->get("/form", "FormsController@index");
}]);

// controller here will be App\Controllers\FormsController
$app->get("/form", "FormsController@index");
```

## Changes

### Handlers now automatically loaded

In earlier versions of Leaf, you were required to call `set404`, `setError` and `setDown` in order to load Leaf's default error screens, however, there's no longer the need to do this unless you want to define a custom screen.

### No need for a constructor

There's no longer a need for a constructor since Leaf router no longer takes in any parameters to set. The easiest way to go with Leaf router now is with static methods. *Even internally, Leaf has switched to using static router methods...shhh, that's a secret!*

## Bug Fixes

### Hook Support

Hooks haven't always been the best way to go when using Leaf router, but now, hooks might end up much more useful in your apps than middleware.

Hooks basically allow you to hook into Leaf router and execute a callback at a given time. For instance, you can execute a function just before Leaf fires off routes. You can also execute a callback before the main middleware executes or even after Leaf has completely executed a route.

There are 6 hooks that you can now use with Leaf router listed below in execution order:

#### router.before

This hook runs before Leaf router begins any operations, even before app middleware are triggered.

#### router.before.route

This hook runs just after the app middleware have run, just before the route specific middleware.

#### router.before.dispatch

This hook runs just before routes are dispatched.

#### router.after.dispatch

This hook runs just after routes are dispatched.

#### router.after.route

This hook runs after Leaf router has finished up with routing and cleaning up, just before the execution of internal code.

#### router.after

This hook runs when leaf completely finishes route execution and cleans up on the internal code as well. This is the last thing Leaf router does before exiting.

**Note** Unlike the above hooks, `router.after` can be directly assigned by passing a function into Leaf router's `run` method.

```php
$app = new Leaf\App;

$app->run(function() {
    echo "Final thing to run";
});
```

Also note that the final function may return a value for further use if need be.

```php
$time = Leaf\Router::run(function() {
    return Leaf\Date::now();
});

saveToLogs("app finished executing", $time);
```

To get started with hooks, simply use the `hook` method to define the hook you want to use.

**It doesn't matter the order in which you define hooks. Leaf router will run them in the correct order.**

```php
$app->hook("router.before", function() {
    Leaf\Http\Headers::resetStatus(202);
});
```

The example above makes sure that every response gets sent with a `202 Accepted` https status instead of the original status code. As you can see, `hook` takes in the hook you wish to set and a callable/callback to execute.

### Route Specific Middleware

Route specific middleware have also received bug fixes and now work as they did before.

```php
$app->before("GET", "/", function() {
    echo "This will run only before the / route";
});
```

### App middleware

App middleware which are created using `Leaf\Middleware` have also received a lot of fixes which make them easier and faster to use.

```php
// usually in a different file
class Test extends Leaf\Middleware
{
    public function call()
    {
        echo "my test middleware";
        
        $this->callNext();
    }
}

$app = new Leaf\App;

$app->add(new Test);
```

## Removed Features

No features have been removed!

## Next Steps

- [Routing](leaf/v/2.5.0/routing/)
- [Dynamic Parameters](leaf/v/2.5.0/routing/dynamic)
- [Sub Routing](leaf/v/2.5.0/routing/sub-routing)
- [Error Handling](leaf/v/2.5.0/routing/errors)
- [Middleware](leaf/v/2.5.0/routing/middleware)

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
