# 🏀 Leaf API Controllers

If you read [creating your first Leaf API](/getting-started/first-app), you should already have an idea on how to work with `Controllers`, but in this section, we'll be going into details.

So basically, we'll be looking at different kinds of controllers, creating controllers and controller methods provided by Leaf Core.

## Generating Controllers

All Leaf API controllers are kept in the `App/Controllers` directory. So you can manually create your own Controller there, but the recommended method is to use the [leaf console tool](/leaf-api/v1.2/utils/console). So, in the root of your leaf API project, open up your console and type:

```bash
php leaf g:controller <Name>
```

**From version 1.2 beta, you no llonger have to fully enter controller names; instead of TodosController, you can enter Todos, or even Todo:**

```bash
php leaf g:controller Todos
```

## A deep look at controllers

As mentioned before, Leaf API has 3 types of controllers: API controllers, resource controllers and web controllers. Though they're all controllers,  they offer different base methods for different purposes.

### Web Controllers

First, let's look at web Controllers. Web controllers extend `Leaf\Controller`. This type of controllers are more suited for general web projects which heavily rely on Views.

To generate a web controller, we just need to add the `-w` flag.

```bash
php leaf g:controller -w <Name>
```

A web controller looks like this:

```php
<?php
namespace App\Controllers;

class ClassName extends \Leaf\Controller {
  //
}
```

This is the default boilerplate generated for the web controller. As mentioned before, Leaf API uses Leaf Core's controller packages which we extend to create our own controller. This provides us with Leaf Core's controller methods. You can read more on the `Leaf\Controller` [here](/2.1/core/controller).

To use this controller to resolve a route, you simply have to pass it into the route like this:

```php
$app->get('/home', '\App\Controllers\ClassName@index');
```

### Resource Controllers

Resource Controllers contain methods to handle CRUD functionality.

```php
<?php
namespace App\Controllers;

class ClassName extends Controller {
  /**
   * Display a listing of the resource.
   */
  public function index() {
    //
  }

  /**
   * Show the form for creating a new resource.
   */
  public function create() {
    //
  }

  /**
   * Store a newly created resource in storage.
   */
  public function store() {
    //
  }

  /**
   * Display the specified resource.
   */
  public function show($id) {
    //
  }

  /**
   * Show the form for editing the specified resource.
   */
  public function edit($id) {
    //
  }

  /**
   * Update the specified resource in storage.
   */
  public function update($id) {
    //
  }

  /**
   * Remove the specified resource from storage.
   */
  public function destroy($id) {
    //
  }
}
```

To generate a resource controller, just add the `-r` flag or `--resource`

```bash
php leaf g:controller <ControllerName> --resource
```

To use this controller to resolve a route, you can map routes to each method manually, but a simpler way would be to use:

```php
$app->resource('/route', '\App\Controllers\ResourceControllerName');
$app->resource('/articles', '\App\Controllers\ArticlesController');
```

### API Controllers

API controllers are the default controllers used in Leaf API.

```bash
php leaf g:controller <ControllerName>
```

```php
<?php
namespace App\Controllers;

class ClassName extends Controller {
    public function index() {
        $this->respond([
            "message" => "This is the ClassName"
        ]);
    }
}
```

This is the default boilerplate generated for the API controller.

### Other Flags

You can also generate a model together with your controller.

```bash
php leaf g:controller <ControllerName> -m
```

Create a template for your controller

```bash
php leaf g:controller <ControllerName> -t
```

Create a model and migration for your  controller

```bash
php leaf g:controller <ControllerName> -a
```

### Controller Help (Leaf Console)

```bash
Description:
  Create a new controller class

Usage:
  g:controller [options] [--] <controller>

Arguments:
  controller            controller name

Options:
  -a, --all             Create a model and migration for controller
  -t, --template        Create a template for controller
      --view            Create a template for controller
  -m, --model           Create a model for controller
  -r, --resource        Create a resource controller
  -w, --web             Create a web controller
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
```

## Next Steps

- [Leaf Core APIControllers](/2.1/core/api-controller)
- [Leaf Core Controllers](/2.1/core/controller)
- [Models](/leaf-api/v1.2/core/models)
- [Migrations](/leaf-api/v1.2/core/migrations)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
