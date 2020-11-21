# Working with controllers

If you read [creating your first LeafMVC app](/first-app/), you should already have an idea on how to work with `controllers`, but in this section, we'll be going into details.

So basically, we'll be looking at different kinds of controllers, creating controllers and controller methods provided by Leaf Core.

# Generating Controllers

With LeafMVC, all controllers are kept in the `app/controllers` directory. So you can manually create your own Controller there, but the recommended method is to use the leaf CMD tool. So, in the root of your leaf MVC project, openup your console and type:
```bash
php leaf g:controller <Name>
```

# A deep look at controllers

As mentioned before, LeafMVC has 3 types of controllers: API controllers, resource controllers and normal controllers. Though they're both controllers,  they offer different base methods for different purposes. For instance, The web controllers come pre-packaged with Leaf Veins.

## Normal Controllers

First, let's look at Normal Controllers.
```php
<?php
    namespace App\Controllers;

    use Leaf\Controller;

    class ClassName extends Controller {
        public function __construct() {
            parent::__construct();
        }

        public function index() {
            $this->set([
                "title" => "Leaf Vein Integration"
            ]);
            $this->render("index");
        }
    }
```
This is the default boilerplate generated for the web controller. As mentioned before, LeafMVC uses Leaf Core's controller packages which we extend to create our own controller. This provides us with Leaf Core's helper methods and Leaf Vein integration. Vein is Leaf's  default templating engine. You can read more on veins [here](/veins/).


To use this controller to resolve a route, you simply have to pass it into the route like this:

```php
$app->get('/home', '\App\Controllers\ClassName@index');
```

## Resource Controllers

Resource Controllers contain methods to handle CRUD functionality.

```php
<?php

namespace App\Controllers;

use Leaf\Controller;
use Leaf\Http\Request;

class ClassName extends Controller {
    public function __construct() {
        parent::__construct();
        $this->request = new Request;
    }
    
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

To generate a resource controller, you can use

```bash
php leaf g:controller <ControllerName> --resource
```

## API Controllers

```php
<?php
    namespace App\Controllers;

    use Leaf\ApiController;

    class ClassName extends ApiController {
        public function __construct() {
            parent::__construct();
        }

        public function index() {
            $this->respond([
				"message" => "This is the ClassName"
			]);
        }
    }
```
This is the default boilerplate generated for the API controller. The API controller has a bunch of handy methods that can be used to handle responses to the user. Some of these are:


`respond()` this takes in an array and displays the data to the user in JSON format


`respondWithCode()` this takes in an array and an HTTP code(integer). It displays the data to the user in JSON format with the HTTP code.

To generate an API controller, you can use
```bash
php leaf g:controller <ControllerName> --api
```

## Others
You can also generate a model together with your controller
```bash
php leaf g:controller <ControllerName> -m
```

Create a template for your controller
```bash
php leaf g:controller <ControllerName> -t
```

Create a model, migration and template foryour  controller
```bash
php leaf g:controller <ControllerName> -a
```


```bash 
g:controller [options] [--] <controller>

Arguments:
  controller            controller name

Options:
  -a, --all             Create a model, migration and template for controller
  -t, --template        Create a template for controller
      --view            Create a template for controller
  -m, --model           Create a model for controller
  -r, --resource        Create a resource controller
      --api             Create an API controller
  -h, --help            Display this help message
```
<br>
<br>

# <a href="#/veins/">Veins</a>
# <a href="#/cmd/">Leaf CMD</a>
# <a href="#/routing/">Routing</a>
# <a href="#/models/">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>