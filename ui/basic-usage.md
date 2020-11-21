# Leaf UI: Basic Usage

This guide assumes you've read the [introduction to Leaf UI](ui/). As said before, Leaf UI is a library for building user interfaces with PHP. In this section we'll be looking at using basic "HTML tags".

A bunch of shorthand methods have been created which allow you use create elements with using the `create_element` we saw before. The mostly look like this:

```php
$ui::div([attributes], [
	// children
]);
```

Now, let's look at our elements.

## Structural HTML Tags

### html

This is the equivalent of `<html>`, it also adds `<!doctype html>` at the begining of the page. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
$ui::html([
	// children here
]);

$ui::html([...], ["lang" => "en-us"]);
```

### head

This is the equivalent of `<head>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
$ui::head([
	// children here
]);
```

### body

This is the equivalent of `<body>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
$ui::body([
	// children here
]);

$ui::body([...], ["style" => "margin: 0;"]);
```

### header

This is the equivalent of `<header>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::header([attributes], [
	// children here
]);
```

### nav

This is the equivalent of `<nav>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::nav([attributes], [
	// children here
]);
```

### footer

This is the equivalent of `<footer>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::footer([attributes], [
	// children here
]);
```

### aside

This is the equivalent of `<aside>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::aside([attributes], [
	// children here
]);
```

### br

This is the equivalent of `<br>`. It takes in just 1 parameter:

- (array, optional) Attributes

```php
$ui::br([attributes]);
```

### hr

This is the equivalent of `<hr>`. It takes in just 1 parameter:

- (array, optional) Attributes

```php
$ui::hr([attributes]);
```

### a

This is the equivalent of `<a>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::a([attributes], [
	// children here
]);
```

### div

This is the equivalent of `<div>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::div([attributes], [
	// children here
]);
```

### span

This is the equivalent of `<span>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::span([attributes], [
	// children here
]);
```

### section

This is the equivalent of `<section>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::section([attributes], [
	// children here
]);
```

### hgroup

This is the equivalent of `<hgroup>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
$ui::hgroup([...], [attributes]);
```

### h1-h6

This is the equivalent of `<h1>`...`<h6>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
$ui::h1([...], [attributes]);
$ui::h3([...], [attributes]);
$ui::h5([...], [attributes]);
```

### blockquote

This is the equivalent of `<blockquote>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
$ui::blockquote([...], [attributes]);
```

### p

This is the equivalent of `<p>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
$ui::p([...], [attributes]);
```

### article

This is the equivalent of `<article>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::article([attributes], [
	// children here
]);
```

### details

This is the equivalent of `<details>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::details([attributes], [
	// children here
]);
```

### summary

This is the equivalent of `<summary>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::summary([attributes], [
	// children here
]);
```

## Meta-data HTML Tags

### title

This is the equivalent of `<title>`. It takes in 2 parameters:

- (string) Title
- (array, optional) Attributes

```php
$ui::title("Home");
```

### Meta

This is the equivalent of `<meta>`. It takes in 3 parameters:

- (string) name `<meta name="">`
- (string) content `<meta content="">`
- (array, optional) Attributes

```php
$ui::meta("viewport", "width=device-width;initial-scale=1");
```

### Link

This is the equivalent of `<link>`. It takes in 3 parameters:

- (string) href `<link href="">`
- (string) rel `<link rel="">`
- (array, optional) Attributes

```php
$ui::link("./style.css", "stylesheet");
```

### [Using Styles](ui/custom-elements?id=_style)

### [Using Scripts](ui/custom-elements?id=_script)

### base

This is the equivalent of `<base>`. It takes in 2 parameters:

- (string) href `<base href="">`
- (array, optional) Attributes

```php
$ui::base("...");
```

## Formatting Tags

### tt

This is the equivalent of `<tt>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
$ui::tt("This is tt");
```

### b

This is the equivalent of `<b>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
$ui::b("...");
```

### i

This is the equivalent of `<i>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
$ui::i("...");
```

### u

This is the equivalent of `<u>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
$ui::u("...");
```

### small

This is the equivalent of `<small>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
$ui::small("...");
```

### sub

This is the equivalent of `<sub>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
$ui::sub("...");
```

### sup

This is the equivalent of `<sup>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
$ui::sup("...");
```

## Embedded Content Tags

### Figure

This is the equivalent of `<figure>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
$ui::figure([attributes], [
	// children here
]);
```

### Img

This is the equivalent of `<img>`. It takes in 2 parameters:

- The image to display
- (array, optional) Attributes

```php
$ui::img("./img.jpg", ["style" => "width: 80px;"]);
```

## Form Tags

### form

This is the equivalent of `<form>`. It takes in 4 parameters:

- (string) method: get, post
- (string) action: where to submit the form
- (array) Form Fields
- (array) attributes for form tag

```php
$ui::form("post", "/form/submit", [
	// children here
]);
```

### input

This is the equivalent of `<input>`. It takes in 3 parameters:

- (string) type: The input type - text, number, password...
- (string) name: Input name `name="..."`
- (array, optional) attributes for input tag

```php
$ui::input("text", "username", [
	"placeholder" => "mychi.darko"
]);
```

`input()` also takes in a `label` attribute which creates a label element.

```php
$ui::input("text", "username", [
	"placeholder" => "mychi.darko",
	"label" => "Enter Your Username"
]);
```

### label

This is the equivalent of `<label>`. It takes in 3 parameters:

- (string) label: The label text
- (string, optional) for: `for="..."`
- (array, optional) attributes for label tag

```php
$ui::label("Enter Your Password", "password");
```

### button

This is the equivalent of `<button>`. It takes in 2 parameters:

- (string) Text on button
- (array, optional) Attributes

```php
$ui::button("Click Me!", ["style" => "background: gold;"]);
```

### [Custom Elements](ui/custom-elements)

<br>
<hr>

<a href="#/ui/basic-usage" style="margin: 0px">Basic Usage</a>
<a href="#/ui/custom-elements" style="margin: 0px 10px;">Custom Elements</a>
<a href="#/2.1-alpha/views/blade" style="margin: 0px; 10px;">Blade Templating</a>
<a href="#/2.1-alpha/http/session" style="margin: 0px 10px;">Session</a>
<a href="#/2.1-alpha/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
