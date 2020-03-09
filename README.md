```js
<?php
require_once __DIR__ . '/vendor/autoload.php';

$leaf = new Leaf\Leaf();

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

# What's new in v2.0?

## Leaf Container
Leaf 2.0 introduces a container as the core of Leaf. This container allows you to use some core packages from leaf without haaving to instanciate them. In previous versions, every single package needed to be initialised. 

This container also allows you to register custom/external packages on the current leaf instance for global use with `$leaf->register()`

```js
	$leaf = new Leaf\App();

	// register a new package
	$leaf->register("purple", function() {
		return new Purple\Leaf();
	});

	$leaf->get("/home", function() use($leaf) {
		// use the purple package
		$something = $leaf->purple->doSomething();
		$leaf->response->respond($something);
	});
```
**View [container docs](2.0/core/container)**

<hr>

## More concise DB Methods
More db methods have been added to Leaf's db packages. These methods provide a simpler and a much more concise way of interacting with your database. Also, the mysqli package has been directly integrated into Leaf core, so you can use it globally without having to instanciate it yourself.

```js
	$leaf = new Leaf\App();
	$form = new Leaf\Form();

	// db connection
	$leaf->db->connect("host", "username", "password", "dbname");

	$leaf->post("/articles/add", function() use($leaf, $form) {
		// validate the data passed in
		$form->validate([
			"title" => "text",
			"author" => "ValidUsername",
			"email" => "email",
			"description" => "text"
		]);

		// insert the data into database, it's sanitised and arranged automatically
		$leaf->db->add("articles", $leaf->request->getBody());

		// return json encoded data
		$leaf->response->respond(
			// same as select * from articles where author = ... with mysqli_fetch_all()
			$leaf->db->choose("articles", ["author" => $form->get("author")])->fetchAll()
		);
	});
```

[Learn more about Leaf Db packages](2.0/db/)

<hr>

## Major Security Fixes
Leaf 2.0 offers full protection from common web app security vulnerabilities like XSS. In Leaf v2, all input is automatically sanitized to make sure no weird scripts get into your application. Let's look at this example.

Considering we have a script `<script>alert("hello");</script>`, we pass this script as a parameter into our app in a post request.

```javascript
$leaf->post('/users/update', function() use($leaf) {
	// without leaf
	echo $_POST["param"];
});
```
In this case, the script is run and the XSS attack is successful.

```javascript
$leaf->post('/users/update', function() use($leaf) {
	// using leaf
	echo $leaf->request->get("param");
});
```
In this case the script is just output to the user as a string.
## [Read the changelog to find all updates in Leaf 2](https://github.com/leafsphp/leaf/blob/v2.0/CHANGELOG.md)

<br>
<hr>

<a href="#/first-app/" style="margin: 0px;">Building your first leaf app</a>
<a href="#/cmd/" style="margin: 0px 10px;">Leaf CMD</a>
<a href="#/routing/" style="margin: 0px 10px;">Routing</a>
<a href="#/controllers/" style="margin: 0px 10px;">Controllers</a>
<a href="#/models/" style="margin: 0px;">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>