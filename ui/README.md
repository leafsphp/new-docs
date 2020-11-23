# Leaf UI <sup style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New</sup>

Leaf UI is a simple UI library for PHP. Leaf UI lets you quickly scaffold webpages without leaving the comfort of PHP; No more writing weird strings, no more weird formatting for HTML inside PHP. One thing to note is that all Leaf UI elements render plain HTML in the browser.

## Simple Example

```php
$ui = new Leaf\UI;

$ui::render($ui::form("method", "action", [
	$ui::h2("Subscribe to my newsletter"),
	$ui::input("type", "name", ["placeholder" => "Enter your email", "label" => "Email"]),
	$ui::button("Get Started", ["type" => "submit"])
]));
```

**OUTPUT:**
<div style="padding: 20px;">
	<form method="method" action="action">
		<h2>Subscribe to my newsletter</h2>
		<label for="21es56">Email</label>
		<input id="21es56" type="type" name="name" placeholder="Enter your email">
		<button type="submit">Get Started</button>
	</form>
</div>

As you've noticed, Leaf UI uses a "function based" syntax, as opposed to traditional HTML tags. This syntax is heavily inspired by [flutter](https://flutter.dev) and [reactjs](//reactjs.org)(without JSX).

## Installation

You can install Leaf UI with composer. Simply run:

```bash
composer require leafs/ui
```

## Basic Concepts

There are a couple of methods which serve as Leaf UI's core: The most important being `create_element`.

### create_element

This method simply allows you to create(render) a native HTML element.

It takes in 4 parameters:

- HTML Element To Render eg: h2 (string, required)

- Element attributes. You can use an empty array if there are no attributes (array, optional)

- Element's Children: can be more Leaf UI components. You can use an empty array if there are no children (array, optional)

- Element type: (optional) This refers to the HTML tag type. Leaf UI supports 3 types:

	- `UI::SINGLE_TAG` for a single tag eg: `meta` and HTML 5 input (`<element attributes>`)

	- `UI::SELF_CLOSING` for a self closing tag `<element attributes />`

	- If the value is not one of the above or this field is left blank, a normal HTML is created `<element attributes>children</element>`

```php
$ui::create_element("h2", ["id" => "title"], [], type)
```

### create_styles

Create styles simply allows you to write styles in your Leaf UI, pretty much like how `<style>` lets you write styles in HTML.

It takes in 2 parameters:

- The styles you want to apply (array)

- Attributes for your style tag when Leaf UI renders in the browser. Leave blank or an empty array if there are no attributes (array)

```php
// no attributes/ class selector
$ui::create_styles([
	".home" => "background: #fefefe;"
], []);

// no attributes/element selector
$ui::create_styles([
	"h2" => "font-family: sans-serif;"
]);

// renders <style type="text/css">
$ui::create_styles([
	"#btn" => "padding: 10px 15px;"
], ["type" => "text/css"]);

// media query example
$ui::create_styles([
	"@media only screen and (max-width: 500px)" => [
		"p > button#btn" => "border: 1px solid grey;"
	]
])
```

Checkout [a simpler alternative to this](ui/custom-elements?id=_style)

### loop

This is an element created to handle loops in your Leaf UI. Since your entire Leaf UI is just a function👌, you can't use "mult-line functions" like `foreach`, `for`, `if`..., therefore, this method has been prepared. It takes in 2 parameters:

- The array to loop through
- A callable handler for loop

The callable should return an element

```php
$users = [
	["name" => "user 1", "rank" => "D"],
	["name" => "user 2", "rank" => "F"],
	["name" => "user 3", "rank" => "S"],
];
// ...
$ui::_row([
	$ui::loop($users, function($user) use($ui) {
		return $ui::_column([
			$ui::h2($user["name"]),
			$ui::small($user["rank"])
		]);
	})
])
```

Also, you can access both the key and value of an array during the loop.

```php
$user = ["name" => "user 1", "rank" => "D"];

$ui::_column([
	$ui::loop($user, function($value, $key) use($ui) {
		return $ui::_row([
			$ui::span("$key:"),
			$ui::h4($value)
		]);
	})
])
```

### random_id

This method as the name suggests, generates a random id. Under the hood Leaf UI uses this method to generate an id for any element which isn't given an id. It takes in 1 param:

- A string to add to id, usually an element name (optional)

```php
$ui::random_id("div");
```

### Render

This method allows you to output the UI you've created into the browser. It takes in 2 parameters:

- The Leaf UI to render
- A string to render before the Leaf UI (optional)

```php
$html = $ui::body([...]);
$ui::render($html);

// or
$ui::render($ui::body([...]));

$ui::render($ui::p("This is a paragraph"), "Something here");
```

### [Basic Usage](ui/basic-usage)

### [Wynter Components](ui/wynter)

### [Custom Elements](ui/custom-elements)

### [Creating Custom Elements](ui/custom-elements?id=creating-your-own-elements)

We need your help developing Leaf UI. You can [contribute to Leaf UI on github](https://github.com/leafsphp/leaf-ui/)

<br>
<hr>

<a href="#/ui/basic-usage" style="margin: 0px">Basic Usage</a>
<a href="#/ui/custom-elements" style="margin: 0px 10px;">Custom Elements</a>
<a href="#/2.1-alpha/views/blade" style="margin: 0px; 10px;">Blade Templating</a>
<a href="#/2.1-alpha/http/session" style="margin: 0px 10px;">Session</a>
<a href="#/2.1-alpha/database" style="margin: 0px 10px;">Using a database</a>

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
