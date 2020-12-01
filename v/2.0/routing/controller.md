# Using Controllers
Controllers are simply classes that serve as bridges between Models and the View part of your application. Don't think too much of controllers, they're nothing but a class. 

In this section, we'll be looking at how to handle a route with a controller. So let's make an example controller: **remember it's just a php class**

```php
<?php
class HomeController {
	public function index() {
		echo "This is the index function";
	}
}
```
To handle a route using this controller, we'll have to import the controller, and then define a simple route

```php
$leaf = new Leaf\App;

require "HomeController.php";

// we leave out the second parameter for now
$leaf->get("/home");
```

When using controllers, instead of defining a closure or function as the second parameter of your route, you rather pass in a string of the controller's class name and the function you want to use. In this case, `"HomeController@index"`, so remember, it's `Class@Method`

```php
$leaf = new Leaf\App;

require "HomeController.php";

$leaf->get("/home", "HomeController@index");
```


## Controller Namespaces
In case you're using an auto loader or using leaf in another framework and  you have your controllers in another directory, you can do sommething like this
```php
$leaf->get('/(\d+)', '\App\Controllers\User@showProfile');
```
But this gets tedious if you have a lot of routes. So Leaf allows you to set a "general" namespace, you can set the default namespace to use on your router instance via `setNamespace()`

```php
$leaf->setNamespace('\App\Controllers');

$leaf->get('/users/(\d+)', 'User@showProfile');
$leaf->get('/cars/(\d+)', 'Car@showProfile');
```

<br>
<hr>

<a href="#/v/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/v/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/v/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>