# Leaf DB

## Introduction

Leaf's "simple query builder" provides a convenient but usual way to quickly create and run database queries. It can be used to perform most database operations in your app.

Leaf's "simple query builder" currently supports Mysqli and PDO connections, though we still recommend using Mysqli. There's no need to worry about SQL injection as parameter binding is also supported and easy to use😉💪

**Note that Leaf v2.1 introduced a new Leaf\Db package which will replace this current query builder completely in later versions of Leaf. Not to worry, `Leaf\Db\Mysqli` and `Leaf\Db\PDO` would be made available through composer**

In v2.1, the Leaf Mysqli package is no longer bound to the Leaf object, so it can't be used without initialising the package.

## Initialising Leaf DB

Leaf DB has 2 different packages, 1 for mysqli and the other for PDO. So you can import which ever package you wish to use. **Leaf recommends using the mysqli package.**

```php
use Leaf\Db\Mysqli;

$db = new Mysqli();

use Leaf\Db\PDO;

$db = new PDO();
```

**Both DB:PDO and DB:Mysqli use the same methods, so all the code below works the same for whichever you're using. We'll alert you if something works differently.**

<hr>

## DB connection

The first thing you need to do to use Leaf DB is to connect to your database. This can be achieved with `connect()`

#### On the leaf object

In v2.1, the default `$app->db` object has been replaced with `Leaf\Db`, therefore, you have to initialise DB Mysqli to use it's methods.

#### DB Mysqli

```php
use Leaf\Db\Mysqli;

$db = new Mysqli();
$db->connect($host, $user, $password, $dbname);
```

#### DB

```php
use Leaf\Db\PDO;

$db = new PDO();
$db->connect($host, $dbname, $user, $password);
```

This will set the connection for use within Leaf DB.

Both packages now support `auto_connect` which allows you to connect to your database using variables set in a `.env` file.

```php
$db->auto_connect();
```

<hr>

## Queries

### Making simple queries
Queries with with Leaf DB are much like what you're used to. Though a query builder, we wan't to maintain the flexibility of normal database queries, hence, we provided the query() method to make your normal database queries.

```php
$db->connect($host, $user, $password, $dbname);

$app->get('/users/all', function() use($app) {
	$users = $db->query("SELECT username FROM users")->fetchAll();
	$app->response->respond($users);
});
```
As normal as this seems, we take it a step further by providing you with a much simpler way to use prepared statements.

```php
$db->connect($host, $user, $password, $dbname);

$app->get('/users/{id}', function($id) use($app) {
	$user = $db->query("SELECT username FROM users WHERE id = ?", [$id])->fetchObj();
	$app->response->respond($user);
});
```

We've looked at making queries, but then `query()` still makes you type out whatever query you need to use. It's certainly easier than raw queries, but it's nothing impressive. Below are some of Leaf DB's handy methods to make queries even easier.💪😉

<hr>

### [Retrieving Data](v/2.4-beta/database/select)

<hr>

### [Inserting Data](v/2.4-beta/database/insert)

<hr>

### Updating Data
This operation uses UPDATE. With Leaf DB:

```php
$db->update();
```

##### Update
We use Leaf DB's update method which takes in a "table", a "column-value" to update and "conditions".

```php
$db->update("posts", "title = 'Post 1'", "title = 'Post One'");
```

This will look for a post with the title of "Post One" and change it to "Post 1".
You can also have multiple conditions:

```php
$db->update("posts", "title = 'Post 1' AND author = 'Mychi Darko'", "title = 'Post One'");
```

##### With Parameter Binding

```php
$db->update("posts", "title = ? AND author = ?", "title = ?", ["Post 1", "Mychi Darko", "Post One"]);
```

<hr>

### Deleting Data
This operation uses DELETE. With Leaf DB:

```php
$db->delete();
```

##### Delete
We use Leaf DB's delete method which takes in a "table", and "conditions".

```php
$db->delete("posts", "title = 'Post 1'");
```

This will look for a post with the title of "Post 1" and delete it.


## Others
### Row Count
Get the number of rows from select

```php
$db->select("posts")->count();
```

### Connection Close
Close the connection

```php
$db->close();
```

<br>
<hr>

<a href="#/v/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/v/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/v/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>