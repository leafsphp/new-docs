# Leaf UI: Basic Usage

This guide assumes you've read the [introduction to Leaf UI](ui/v/0.1.0/). As said before, Leaf UI is a library for building user interfaces with PHP. In this section we'll be looking at using basic "HTML tags".

A bunch of shorthand methods have been created which allow you use create elements with using the `create_element` we saw before. The mostly look like this:

```php
div([attributes], [
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
html([
  // children here
]);

html([...], ["lang" => "en-us"]);
```

### head

This is the equivalent of `<head>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
head([
  // children here
]);
```

### body

This is the equivalent of `<body>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
body([
  // children here
]);

body([...], ["style" => "margin: 0;"]);
```

### _header

This is the equivalent of `<header>`. It uses _ to differentiate itself from the default PHP function `header`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
_header([attributes], [
  // children here
]);
```

### nav

This is the equivalent of `<nav>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
nav([attributes], [
  // children here
]);
```

### footer

This is the equivalent of `<footer>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
footer([attributes], [
  // children here
]);
```

### aside

This is the equivalent of `<aside>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
aside([attributes], [
  // children here
]);
```

### br

This is the equivalent of `<br>`. It takes in just 1 parameter:

- (array, optional) Attributes

```php
br([attributes]);
```

### hr

This is the equivalent of `<hr>`. It takes in just 1 parameter:

- (array, optional) Attributes

```php
hr([attributes]);
```

### a

This is the equivalent of `<a>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
a([attributes], [
  // children here
]);
```

### div

This is the equivalent of `<div>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
div([attributes], [
  // children here
]);
```

### span

This is the equivalent of `<span>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
span([attributes], [
  // children here
]);
```

### section

This is the equivalent of `<section>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
section([attributes], [
  // children here
]);
```

### hgroup

This is the equivalent of `<hgroup>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
hgroup([...], [attributes]);
```

### h1-h6

This is the equivalent of `<h1>`...`<h6>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
h1([...], [attributes]);
h3([...], [attributes]);
h5([...], [attributes]);
```

### blockquote

This is the equivalent of `<blockquote>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
blockquote([...], [attributes]);
```

### p

This is the equivalent of `<p>`. It takes in 2 parameters:

- (array) Children
- (array, optional) Attributes

```php
p([...], [attributes]);
```

### article

This is the equivalent of `<article>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
article([attributes], [
  // children here
]);
```

### details

This is the equivalent of `<details>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
details([attributes], [
  // children here
]);
```

### summary

This is the equivalent of `<summary>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
summary([attributes], [
  // children here
]);
```

## Meta-data HTML Tags

### title

This is the equivalent of `<title>`. It takes in 2 parameters:

- (string) Title
- (array, optional) Attributes

```php
title("Home");
```

### Meta

This is the equivalent of `<meta>`. It takes in 3 parameters:

- (string) name `<meta name="">`
- (string) content `<meta content="">`
- (array, optional) Attributes

```php
meta("viewport", "width=device-width;initial-scale=1");
```

### _link

This is the equivalent of `<link>`. It takes in 3 parameters:

- (string) href `<link href="">`
- (string) rel `<link rel="">`
- (array, optional) Attributes

```php
_link("./style.css", "stylesheet");
```

### [Using Styles](ui/v/0.1.0/custom-elements?id=style)

### [Using Scripts](ui/v/0.1.0/custom-elements?id=script)

### base

This is the equivalent of `<base>`. It takes in 2 parameters:

- (string) href `<base href="">`
- (array, optional) Attributes

```php
base("...");
```

## Formatting Tags

### tt

This is the equivalent of `<tt>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
tt("This is tt");
```

### b

This is the equivalent of `<b>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
b("...");
```

### i

This is the equivalent of `<i>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
i("...");
```

### u

This is the equivalent of `<u>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
u("...");
```

### small

This is the equivalent of `<small>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
small("...");
```

### sub

This is the equivalent of `<sub>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
sub("...");
```

### sup

This is the equivalent of `<sup>`. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
sup("...");
```

## Embedded Content Tags

### Figure

This is the equivalent of `<figure>`. It takes in 2 parameters:

- (array, optional) Attributes
- (array) Children

```php
figure([attributes], [
  // children here
]);
```

### Img

This is the equivalent of `<img>`. It takes in 2 parameters:

- The image to display
- (array, optional) Attributes

```php
img("./img.jpg", ["style" => "width: 80px;"]);
```

## Form Tags

### form

This is the equivalent of `<form>`. It takes in 4 parameters:

- (string) method: get, post
- (string) action: where to submit the form
- (array) Form Fields
- (array) attributes for form tag

```php
form("post", "/form/submit", [
  // children here
]);
```

### input

This is the equivalent of `<input>`. It takes in 3 parameters:

- (string) type: The input type - text, number, password...
- (string) name: Input name `name="..."`
- (array, optional) attributes for input tag

```php
input("text", "username", [
  "placeholder" => "mychi.darko"
]);
```

`input()` also takes in a `label` attribute which creates a label element.

```php
input("text", "username", [
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
label("Enter Your Password", "password");
```

### button

This is the equivalent of `<button>`. It takes in 2 parameters:

- (string) Text on button
- (array, optional) Attributes

```php
button("Click Me!", ["style" => "background: gold;"]);
```

### [Custom Elements](ui/v/0.1.0/custom-elements)

<br>
<hr>

<a href="#/ui/v/0.1.0/basic-usage" style="margin: 0px">Basic Usage</a>
<a href="#/ui/v/0.1.0/custom-elements" style="margin: 0px 10px;">Custom Elements</a>
<a href="#/2.1-alpha/views/blade" style="margin: 0px; 10px;">Blade Templating</a>
<a href="#/2.1-alpha/http/session" style="margin: 0px 10px;">Session</a>
<a href="#/2.1-alpha/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
