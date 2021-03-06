# 🥇 Your First Leaf App

## 📄 Hello World

First of all, we need to setup our .htaccess file. See [Re-routing to index.](leaf/v/2.1/intro/htaccess)

To create a hello world project with Leaf, you simply need to initialise Leaf. This will spin up Leaf's core packages. Amongst the core packages is Leaf's router. This simply takes all requests coming into the application and handles them based on rules you define. Enough talk, let's get dirty.

```php
// import composer's autoloader
require_once __DIR__ . "/vendor/autoload.php";

// initialise leaf
$leaf = new Leaf\App();

$leaf->get('/', function() {
	echo "Hello World";
});

$leaf->run();
```

That's all. It's this simple.

This is a very basic example, if you want to explore deeper, more useful examples, you can check out our [code labs](codelabs/) section

<br>
<hr>

<a href="#/leaf/v/2.1/http/request" style="margin: 0px">Request</a>
<a href="#/leaf/v/2.1/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/leaf/v/2.1/routing" style="margin: 0px; 10px;">Routing</a>
<a href="#/leaf/v/2.1/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/leaf/v/2.1/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>