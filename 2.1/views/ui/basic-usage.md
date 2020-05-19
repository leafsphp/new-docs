# Leaf UI: Basic Usage <sup style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2.1</sup>

This guide assumes you've read the [introduction to Leaf UI](2.1/views/ui/). As said before, Leaf UI is a library for building user interfaces with PHP. In this section we'll be looking at using basic "HTML tags".

A bunch of shorthand methods have been created which allow you use create elements with using the `create_element` we saw before. The mostly look like this:

```js
$ui::div([attributes], [
	// children
]);
```

Now, let's look at our elements.

## General HTML Stuff

### HTML

This is the equivalent of `<html>`, it also adds `<!doctype html>` at the begining of the page. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```js
$ui::html([
	// children here
]);
```

### Head

This is the equivalent of `<head>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```js
$ui::head([
	// children here
]);
```

#### Title

This is the equivalent of `<title>`. It takes in 2 parameters:

- (string) Title
- (array, optional) Attributes

```js
$ui::title("Home");
```

#### Meta

This is the equivalent of `<meta>`. It takes in 3 parameters:

- (string) name `<meta name="">`
- (string) content `<meta content="">`
- (array, optional) Attributes

```js
$ui::meta("viewport", "width=device-width;initial-scale=1");
```

#### Link

This is the equivalent of `<link>`. It takes in 3 parameters:

- (string) href `<link href="">`
- (string) rel `<link rel="">`
- (array, optional) Attributes

```js
$ui::link("./style.css", "stylesheet");
```

#### [Using Styles](2.1/views/ui/custom-elements?id=_style)

#### [Using Scripts](2.1/views/ui/custom-elements?id=_script)

### Body

This is the equivalent of `<body>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```js
$ui::body([
	// children here
]);
```

### Header

This is the equivalent of `<header>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```js
$ui::header([attributes], [
	// children here
]);
```

### Footer

This is the equivalent of `<footer>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```js
$ui::footer([attributes], [
	// children here
]);
```

### Aside

This is the equivalent of `<aside>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```js
$ui::aside([attributes], [
	// children here
]);
```

### Img

This is the equivalent of `<img>`. It takes in 1 parameter:

- (array, optional) Attributes

```js
$ui::img(["src" => "./img.jpg"]);
```

### Figure

This is the equivalent of `<figure>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```js
$ui::figure([attributes], [
	// children here
]);
```

### a

This is the equivalent of `<a>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```js
$ui::a([attributes], [
	// children here
]);
```

### Div

This is the equivalent of `<div>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```js
$ui::div([attributes], [
	// children here
]);
```

### span

This is the equivalent of `<span>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```js
$ui::span([attributes], [
	// children here
]);
```

### section

This is the equivalent of `<section>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```js
$ui::section([attributes], [
	// children here
]);
```

### article

This is the equivalent of `<article>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```js
$ui::article([attributes], [
	// children here
]);
```

### Typography

#### h1-h6

This is the equivalent of `<h1> - <h6>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```js
$ui::h1(["style" => "color: red"], [
	// children here
]);

$ui::h6([attributes], [
	// children here
]);
```

### blockquote

This is the equivalent of `<blockquote>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```js
$ui::blockquote("This is a blockquote");
$ui::blockquote([
	$ui::b("Text Here")
]);
```

### tt

This is the equivalent of `<tt>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```js
$ui::tt("This is tt");
```

### b

This is the equivalent of `<b>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```js
$ui::b("This is a bold text", ["style" => "color: red;"]);
```

### i

This is the equivalent of `<i>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```js
$ui::i("This is italics");
```

### u

This is the equivalent of `<u>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```js
$ui::u("This is underlined txt");
```

### sub

This is the equivalent of `<sub>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```js
$ui::sub("This is a subscript");
```

### sup

This is the equivalent of `<sup>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```js
$ui::sup("This is a superscript");
```

### uppercase

Makes all takes uppercase. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```js
$ui::uppercase("This is uppercase");
```

### lowercase

Makes all text lowercase. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```js
$ui::lowercase("This is a lowercase");
```

### p

This is the equivalent of `<p>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```js
$ui::p("This is a paragraph");
```

## Form Elements

This is a section that deals with form components.

### form

This is the equivalent of `<form>`. It takes in 4 parameters:

- (string) method: get, post
- (string) action: where to submit the form
- (array) Form Fields
- (array) attributes for form tag

```js
$ui::form("post", "/form/submit", [
	// children here
]);
```

### input

This is the equivalent of `<input>`. It takes in 3 parameters:

- (string) type: The input type - text, number, password...
- (string) name: Input name `name="..."`
- (array, optional) attributes for input tag

```js
$ui::input("text", "username", [
	"placeholder" => "mychi.darko"
]);
```

`input()` also takes in a `label` attribute which creates a label element.

```js
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

```js
$ui::label("Enter Your Password", "password");
```

### [Custom Elements](2.1/views/ui/custom-elements)

<br>
<hr>

<a href="#/2.1/views/ui/basic-usage" style="margin: 0px">Basic Usage</a>
<a href="#/2.1/views/ui/custom-elements" style="margin: 0px 10px;">Custom Elements</a>
<a href="#/2.1/views/blade" style="margin: 0px; 10px;">Blade Templating</a>
<a href="#/2.1/http/session" style="margin: 0px 10px;">Session</a>
<a href="#/2.1/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
