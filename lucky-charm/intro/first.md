# 🥇 Your First Leaf App

## 📄 Hello World

First of all, we need to setup our .htaccess file. See [Re-routing to index.](lucky-charm/intro/htaccess)

To create a hello world project with Leaf, you simply need to initialise Leaf. This will spin up Leaf's core packages. Amongst the core packages is Leaf's router. This simply takes all requests coming into the application and handles them based on rules you define. Enough talk, let's get dirty.

```php
// import composer's autoloader
require_once __DIR__ . "/vendor/autoload.php";

// initialise leaf
$app = new Leaf\App;

$app->get('/', function() {
  echo "Hello World";
});

$app->run();
```

That's all. It's this simple.

This is a very basic example, if you want to explore deeper, more useful examples, you can check out our [code labs](codelabs/) section

<br>
<hr>

<a href="#/lucky-charm/http/request" style="margin: 0px">Request</a>
<a href="#/lucky-charm/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/lucky-charm/routing" style="margin: 0px; 10px;">Routing</a>
<a href="#/lucky-charm/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/lucky-charm/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>