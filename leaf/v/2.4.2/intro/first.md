# Your First Leaf App

## 📄 Hello World

First of all, we need to setup our .htaccess file. See [configuring .htaccess](leaf/v/2.4.2/intro/htaccess)

To create a hello world project with Leaf, you simply need to initialise Leaf. This will spin up Leaf's core packages. Amongst the core packages is Leaf's router. This simply takes all requests coming into the application and handles them based on rules you define. Enough talk, let's get dirty.

```php
// import composer's autoloader
require_once __DIR__ . "/vendor/autoload.php";

// initialise leaf
$app = new Leaf\App;

$app->get('/', function() use($app) {
  $app->response()->json([
    "message" => "Hello World"
  ]);
});

$app->run();
```

That's all. It's this simple. Let's quickly run through some important parts of Leaf, you'll have to refer to the individual documentations to view all features.

You might have seen it above, but you can use [response](leaf/v/2.4.2/http/response) on `$app`, you can also do the same with [request](leaf/v/2.4.2/http/request). Basically, response let's you deal with output, while request deals with input into your app.

```php
$app->get("/user", function() use($app) {
  $name = $app->request()->get("name");

  $app->response()->json([
    "name" => $name
  ]);
});
```

The example above retrieves a get request param: `name`, sets it into a variable and outputs it as a json object. The URI for the above example would be something like `/user?name=mychi`. You can read more on request and response for more functionality.

Leaf also has a simple package for working with databases. It's really easy to use and doesn't even need you to know sql for basic use cases. Let's follow the example above, but this time, we'll save the name as a new user.

```php
// get name from request
// $name = $app->request()->get("name");

// a better way to do it...when working with multiple params
$data = $app->request()->get(["name"]);

// This is an array of items which shouldn't already exist in the db
$uniques = ["name"];

// The table to add user
$table = "users";

// initialize Leaf Db. You can connect on init
$db = new Leaf\Db("host", "user", "pass", "dbName");

// make our query
$success = $db->insert($table)->params($data)->unique($uniques)->execute();

// catch errors if query fails
if (!$success) {
  // throwErr outputs json and stops the app
  $app->response()->throwErr(
    // most leaf modules have the errors() method which returns errors if any
    $db->errors()
  );
}

// We can fetch the user we just saved
$user = $db->select($table)->where($data)->hidden(["id"])->first();

$app->response()->json(["name" => $user]);
```

Leaf Db provides a ton of features ready for use anywhere in your app. [Read the docs here](leaf/v/2.4.2/db/)

Although Leaf Db is very easy, user authentication can get quite tricky depending on your app, there's also JWT concerns and stuff like that which Leaf Db can't handle...good news, Leaf has the right module for this.

[Auth](leaf/v/2.4.2/core/auth) is a module created to make authentication as simple as 1 line of code. Yes, 1 line😆

Rewriting the example above will look like this:

```php
$data = $app->request()->get(["name"]);

// This is an array of items which shouldn't already exist in the db
$uniques = ["name"];

// The table to add user
$table = "users";

// initialize Leaf Auth.
$auth = new Leaf\Auth;

// connect database
$auth->connect("host", "user", "pass", "dbName");

// Save and retrieve user with JWT created. In 1 line.
$user = $auth->register($table, $data, $uniques);

if (!$user) {
  $app->response()->throwErr(
    // most leaf modules have the errors() method which returns errors if any
    $auth->errors()
  );
}

$app->response()->json($user);
```

This is a very basic example, if you want to explore deeper, more useful examples, you can check out our [code labs](codelabs/) section

<br>
<hr>

## Next steps

- [Leaf Config](leaf/v/2.4.2/config/)
- [Routing](leaf/v/2.4.2/routing/)
- [Request](leaf/v/2.4.2/http/request)
- [Response](leaf/v/2.4.2/http/response)

<br>

Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
