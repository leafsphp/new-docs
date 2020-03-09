# Leaf Veins
Leaf Vein is the official templating engine of Leaf PHP. It focuses on keeping things simple and elegant. It comes pre-packaged with Leaf Core, which is the base of LeafMVC.
Vein files are saved as `.vein.php`.

**This tutorial is about Veins...not just LeafMVC**


# Syntax
Let's take this simple example. Consider this folder structure
```bash
C:.
├───app
│   ├───controllers
│   ├───views
```
In our views, we can create `index.vein.php` which is going to be our view. Sample index.vein.php
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
Then in our controllers folder, we can have index.php.
```javascript
<?php

class Home  {
	public function index() {
		// something here
	}
}
```

In order to use Veins in this class, we'll have to import it from Leaf Core

```javascript
use Leaf\Veins\Template;

class Home extends Template {
	public function index() {
		// something here
	}
}
```
Now, we can use Leaf Vein in this class. But first, check-out

```javascript
$user = (object) [
	'name' => 'Jane Doe',
	'email' => 'janedoe@gmail.com',
	'verified' => true
];
```

In order to use this object in our view, we'd have to pass this object through `set()` and then render our view
```javascript
$this->set(["name" => $user->name]);
$this->render("app/views/index");
```

Then we can access it with 
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
```javascript
$this->set([
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
<br>

# <a href="#/cmd/">Leaf CMD</a>
# <a href="#/models/">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>