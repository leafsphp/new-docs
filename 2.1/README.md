# Getting Started

## Leaf PHP v2.1

Leaf v2.1 is the latest release of Leaf PHP Framework that comes along with a bunch of new features, better functionality and fixes from the previous version.

## Installation

You can view installation for Leaf v2.1 [here](2.1/intro/)

## What's New

### Leaf UI [BETA]

Leaf UI is a simple UI Framework for PHP. Okay, that sounds weird😂. Leaf UI simply lets you create user interfaces without leaving the comfort of PHP. With a [flutter](https://flutter.dev)-like structure, Leaf UI is really easy to pick up and use, even when compared with HTML.

```js
// Leaf UI Package (Not necessary to initialise)
$ui = new Leaf\UI;

// Create your Leaf UI
$html = $ui::html([
	$ui::head([
		$ui::title("Home"),
		$ui::meta("viewport", "width=device-width;initial-scale=1"),
		$ui::_style("./style.css"),
		$ui::_style([
			"@media only screen and (max-width: 600px)" => [
				".ui:row" => "flex-direction: column;"
			]
		])
	]),
	$ui::body(["style" => "background: #cecece;"], [
		$ui::_row([], [
			$ui::_column(["style" => "width: 50%"], [
				// Information Here
			]),
			$ui::_column(["style" => "width: 50%"], [
				$ui::form("method", "action", [
					$ui::input("text", "username", [
						"placeholder" => "mychi.darko",
						"label" => "Enter Your Username"
					]),
					$ui::input("password", "password", [
						"placeholder" => "********",
						"label" => "Enter Your Password"
					]),
					$ui::button("LOGIN NOW", ["type" => "submit"])
				])
			])
		])
	])
]);

// render your Leaf UI
$ui::render($html);
```

[Read Leaf UI Docs](2.1/views/ui/)

### Route::resource

This is a new method inspired by [laravel](http://laravel.com/)'s resource route. This simply let's you create a route handled by a resource controller.

```js
$app = new Leaf\App();

$app->resource("/posts", "PostController");

$app->run();
```

[Read Routing Docs](2.1/routing/controller)

### Session::retrieve

<br>
<hr>

<a href="#/2.1intro/htaccess" style="margin: 0px;">Re-routing to index</a>
<a href="#/2.1intro/first" style="margin: 0px 10px;">Building your first leaf app</a>
<a href="#/2.1routing/" style="margin: 0px 10px;">Routing</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>