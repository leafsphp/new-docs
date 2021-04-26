# Changes in Leaf router

Leaf router has seen huge improvements, usability upgrades, bug fixes and of course new features. This page was created to give you a fair idea of what these changes are and how to use them.

## New Features

### Named routes

You can give route names which you can call them with instead of using the path (Inspired by vue-router). To name a route, simply call `name` followed by the route. **Note that `name` must only be used before the route you wish to name.**

```php
$app->name("home")->get("/home", function() {
  echo "User Home";
});
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

You can now select namespaces for individual groups of routes. Usually, a namespace is given to all your routes, however, a group may need a different namespace for it's controllers and that is what Leaf gives you. To get started simply call `namespace` on the group you wish, it in no way affects the operations of `setNamespace`.

**You should only use `namespace` infront of the group you want to use.**

```php
$app->setNamespace("App\Controllers");

$app->namespace("Lib\Controllers")->group("/user", function() use($app) {
    // controller here will be Lib\Controllers\FormsController
    $app->get("/form", "FormsController@index");
});

// controller here will be App\Controllers\FormsController
$app->get("/form", "FormsController@index");
```

### Group prefixes

Prefixes allow you to add to a group's base path.

```php
$app->prefix("/prefix")->group("/user", function() use($app) {
    // --------> /prefix/user
    $app->get("/", function() use($app) {
        // ...
    });
});
```

## Changes

### Handlers now automatically loaded

In earlier versions of Leaf, you were required to call `set404`, `setError` and `setDown` in order to load Leaf's default error screens, however, there's no longer the need to do this unless you want to define a custom screen.

### No need for a constructor

There's no longer a need for a constructor since Leaf router no longer takes in any parameters to set. Also, although you can use Leaf router with static methods, it's better to initilize it (if you want to use new features like `name` and `namespace`)

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
