```js
<?php
require_once __DIR__ . '/vendor/autoload.php';

$leaf = new Leaf\App;

$leaf->set404();

$leaf->db->connect("host", "username", "password", "dbname");
					
$leaf->get('/book/{id}', function($id) use($leaf) {
	$leaf->response->respond(["id" => $id]);
});

$leaf->get('/home', function() use($leaf) {
	$leaf->response->renderPage('./index.html');
});

$leaf->post('/books/add', function() use($leaf) {
	$title = $leaf->request->get('title');
	$leaf->db->add("books", ["title" => $title], ["title"]);
	$leaf->response->respond([
		"books" => $leaf->db->select("books")->fetchAll()
	]);
});

$leaf->run();
```

# Quickly Create PHP Projects

Leaf is a PHP framework that helps you create clean, simple but powerful web apps and APIs quickly. Leaf introduces a cleaner and much simpler structure to the PHP language while maintaining it's flexibility. With a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant web apps and APIs.💪
<br>
<br>
<br>

## Installation

You can quickly get leaf installed in your application using composer. Simply run:

```bash
composer require leafs/leaf
```

You can then import leaf into your project and start building all your amazing projects. You can view your project using:

```bash
php -S localhost:8080
```

## Working with MVC

Although leaf on it's own isn't an MVC framework, it contains useful tools and packages which allow you to use Leaf as any other MVC framework.

If however, you want an already built MVC setup with scaffolding and a whole lot of other amazing features, you can try out [Leaf MVC](//leafmvc.netlify.app).

Leaf MVC provides an MVC wrapper around Leaf itself. So you can use all of Leaf's cool features alongside a nice set of development tools offered by Leaf MVC.

Although Leaf MVC is useable, there's still a lot of work to be done on it. You can also help with it's development.

**Checkout [Leaf MVC](//leafmvc.netlify.app).**

## Leaf UI

Leaf UI is a php framework for building user interfaces😅. As weird as this sounds, this is another project being actively developed.

Leaf UI allows you to focus almost entirely on writing your php application. Instead of having to build interfaces with html, with weird formatting and string interpolations everywhere, Leaf UI gives you a PHP replacement.

Not only does it allow you skip annoying HTML, but also with integrations like [wynter](https://github.com/leafsphp/leaf-ui/tree/wynter), you can write fully-powered Leaf UI apps without touching HTML, CSS or JavaScript. Amazing, right?

```js
$ui = new Leaf\UI\Template;

$users = [
	["name" => "User 1"],
	["name" => "User 2"],
	["name" => "User 3"]
];

$html = $ui::_template("Page Title", [
	$ui::_container([
		$ui::_row([
			$ui::loop($users, function($user) use($ui) {
				return $ui::div(["style" => "background: #fcfcfd;"], [
					$ui::h3($user["name"])
				]);
			})
		])
	])
]);

$ui::render($html);
```

**[Read the docs](ui/)**

As amazing as Leaf UI is, it's still under development and has a whole lot of work left to be done. [Contribute to the Leaf UI project on github.](https://github.com/leafsphp/leaf-ui)

## Leaf API

This is another project based on Leaf PHP. Just like Leaf MVC, Leaf API is a wrapper around Leaf which allows you use MVC features, but built with APIs in mind. This is like the [Lumen](https://lumen.laravel.com/) to [Laravel](https://laravel.com/)

**Contribute to [Leaf API](https://github.com/leafsphp/leafAPI).**

<br>
<hr>

<a href="#/2.0/intro/first" style="margin-right: 10px;">Building your first leaf app</a>
<a href="#/2.0/routing/" style="margin: 0px 10px;">Routing</a>
<a href="#/2.0/core/controller" style="margin: 0px 10px;">Controllers</a>
<a href="#/2.0/core/model" style="margin: 0px 10px;">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>