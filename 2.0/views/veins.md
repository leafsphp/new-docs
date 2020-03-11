# Leaf Veins
Leaf Veins templating engine is the official templating engine of Leaf PHP. It focuses on keeping things simple and elegant. For those who have used **Smarty** before, this will be really easy to get used to.

Remember, all vein files end with `.vein.php`
### Sample Vein File
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>{$title}</title>
	<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
</head>
<body>
	<h2>{$title}</h2>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script>
</body>
</html>
```

<hr>

## Intro

To use veins, you can initialise the `Leaf\Veins` class, or call it directly since it's bound on the Leaf object.

### Leaf\Veins init
```js
$veins = new Leaf\Veins();
```

### With Leaf Object <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 12px;">New in v2</span></sup>
```js
$veins = $leaf->veins;
```

## Quick Walk-through
This is a simple "tutorial" to get you up and going with Leaf Veins. The whole idea is to be able to pass items into our view(template).

Imagine this object
```js
$user = (object) [
	'name' => 'Michael Darko',
	'email' => 'mickdd22@gmail.com',
	'verified' => true
];
```

In order to use this object in our view(template), we'd have to pass this object through `set()` and then render our view. `set()` is a special method that passes values directly into out template.
```js
// pass single value to template
$leaf->veins->set("name", $user->name);

// pass multiple values
$leaf->veins->set(["name" => $user->name, "email" => $user->email]);
```

Now that our data has been set, we'll need to render this our template which the data is getting passed into. But before that, we'll have to tell Veins where to look for our templates and what directory to keep the template cache in. We can do this with `configure`.

```js
$leaf->veins->configure([
	"veins_dir" => "views/",
	"cache_dir" => "views/cache/"
]);
```

There are many more configurations available. This is an array of Veins default configurations, you can configure based on these.

```js
[
	'checksum' => array(),
	'charset' => 'UTF-8',
	'debug' => false,
	'veins_dir' => 'views/',
	'cache_dir' => 'cache/',
	'base_url' => '',
	'php_enabled' => false,
	'auto_escape' => true,
	'sandbox' => true,
	'remove_comments' => false
];
```

Now that we've set the template and cache directories, we can now render our template

```js
$leaf->veins->render("homepage"); // homepage.vein.php
```

Now in our homepage.vein.php file, we can access the name variable like this:

```html
{$name}
```

## Variables
```html
{$variable}
{$object.key}
{$object->key}
{$array->key}
```

## Connstants
```html
{#constant#}
```

## Function
```html
{function="function"}
```

## Include
```html
{include="templateName"}
```

## No parse
Commenting in Vein
```html
{noparse}
	code
{/noparse}
```

## Loops
```html
{loop="$items" as $item}
	<div style="margin-bottom: 50px;">
		<h3><a href="/items/{$item->id}">{$item->title}</a></h3>
		<p>{$item->body}</p>
	</div>
{/loop}
```

Or 

```html
{loop="$items"}
	<div style="margin-bottom: 50px;">
		<h3><a href="/items/{$value->id}">{$value->title}</a></h3>
		<p>{$value->body}</p>
	</div>
{/loop}
```

## If
```html
{if="count($posts) > 0"}
	All Posts
{/if}
```

## If else
```html
{if="count($posts) > 0"}
	All Posts
{else}
	There are no posts
{/if}
```

## AutoEscape
This has a lot of uses...but the most common use case is for rendering HTML
```js
$leaf->veins->set([
	"post" => [
		"body" => "<h2>This is the body</h2>"
	]
]);
```
```html
{autoescape="off"}
	{$post.body}
{/autoescape}
```

<br>
<hr>

<a href="#/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>