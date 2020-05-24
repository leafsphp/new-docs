# Leaf UI <sup style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2.1 alpha</sup>

Leaf UI is a simple UI library for PHP. Leaf UI lets you quickly scaffold webpages without leaving the comfort of PHP; No more writing weird strings, no more weird formatting for HTML inside PHP. One thing to note is that all Leaf UI elements render plain HTML in the browser.

## Simple Example

```js
$ui = new Leaf\UI;

$ui::render($ui::form("method", "action", [
	$ui::_text("Subscribe to my newsletter", ["size" => "22px"]),
	$ui::input("type", "name", ["placeholder" => "Enter your email", "label" => "Email"]),
	$ui::button("Get Started", ["type" => "submit"])
]));
```

This code above simply renders a form with an `input` and `button` and a info text above the form fields which says "Subscribe to my newsletter".

Now compare this to it's equivalent in ordinary PHP

```js
echo '
<form method="method" action="action">
	<p style="margin: 0px; font-size: 22px">Subscribe to my newsletter</p>
	<label>Email</label>
	<input type="type" name="name" placeholder="Enter your email">
	<button type="submit">Get Started</button>
</form>';
```

As you've noticed, Leaf UI uses a "function based" syntax, as opposed to traditional HTML tags. This syntax is heavily inspired by [flutter](https://flutter.dev) and [reactjs](//reactjs.org)(without JSX).

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

```js
$ui::create_element("h2", ["id" => "title"], [], type)
```

### create_styles

Create styles simply allows you to write styles in your Leaf UI, pretty much like how `<style>` lets you write styles in HTML.

It takes in 2 parameters:

- The styles you want to apply (array)

- Attributes for your style tag when Leaf UI renders in the browser. Leave blank or an empty array if there are no attributes (array)

```js
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

Checkout [a simpler alternative to this](2.1-alpha/views/ui/custom-elements?id=_style)

### Render

This method allows you to output the UI you've created into the browser.

```js
$html = $ui::body([...]);
$ui::render($html);

// or
$ui::render($ui::body([...]));
```

### [Basic Usage](2.1-alpha/views/ui/basic-usage)

### [Custom Elements](2.1-alpha/views/ui/custom-elements)

### [Creating Custom Elements](2.1-alpha/views/ui/custom-elements?id=creating-your-own-elements)

<br>
<hr>

<a href="#/2.1-alpha/views/ui/basic-usage" style="margin: 0px">Basic Usage</a>
<a href="#/2.1-alpha/views/ui/custom-elements" style="margin: 0px 10px;">Custom Elements</a>
<a href="#/2.1-alpha/views/blade" style="margin: 0px; 10px;">Blade Templating</a>
<a href="#/2.1-alpha/http/session" style="margin: 0px 10px;">Session</a>
<a href="#/2.1-alpha/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
