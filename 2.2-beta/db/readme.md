# 📑 Leaf Db <sup><small style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2.1</small></sup>

Leaf Db is a new lightweight but powerful query builder which allows you quickly write dynamic queries, validate and seperate data in just a single line of code.

In later versions of Leaf, Leaf Db will be completely replacing the database packages used earlier: `Leaf\Db\Mysqli` and `Leaf\Db\PDO`. Of course, you'll be able to install them using composer.

## 📖 Getting Started

There are 2 ways to use Leaf Db in your application. The first way would be to just call whatever method you need on the main db object.

```php
$app = new Leaf\App;
$app->db->auto_connect();
```

Alternatively, you could initialise it just like any other Leaf package, then call whatever method you need.

```php
$db = new Leaf\Db;
$db->auto_connect();
```

## 😵 Db Connection

The first thing to always do is to connect to your database. Since all db operations are performed on the database, you can't do without it.

There are 3 ways to connect your database.

### connect on init

This method connects to the database when initializing Leaf Db.

```php
$db = new Leaf\Db("db_host", "user", "password", "db_name");
```

### connect

Connect takes in 4 params just like the method above

```php
$db = new Leaf\Db;
$db->connect("db_host", "user", "password", "db_name");
```

### auto_connect

This method allows you to connect to your database from parameters in a `.env` file. Most MVC frameworks and other libraries rely on a `.env` for a lot of configurations including the database. With `auto_connect`, you can directly pick up these configs.

**example env:**

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=LeafMVC
DB_USERNAME=root
DB_PASSWORD=
```

**App:**

```php
$db = new Leaf\Db;
$db->auto_connect();
```

## ❔ Queries

### Making simple queries

Leaf Db provides a ton of functionality, with a bunch of powerful tools, but at the same time gives you a great deal of customizations with the `query` method.

```php
$users = $db->query("SELECT * FROM users")->fetchAll();
```

You can also use parameter binding with `query`

```php
$db->query("SELECT * FROM users WHERE id = ?")->bind("1")->fetchObj();
```

A shorter method would be to use `where`

```php
$db->query("SELECT * FROM users")->where("id", "1")->fetchObj();
```

You don't have to worry about security, where uses prepared statements by default, so you're pretty good.

You've seen all this, but guess what? There's something even shorter😵

```php
$db->select("users")->where("id", "1")->fetchObj();
```

This is what Leaf Db does for you. A new way to write your Database queries without actually needing to write any real queries. Also, unlike other query builders, there's no need to create classes and models for every table you want to fetch from. Everything's accessible with one line of code💖

### 🖐 select

As you saw in the example above, `select` makes writing select statements really simple.

It takes in 2 parameters:

- The table to select items from
- The columns to include (includes all by default)

```php
// returns all items
$items = $db->select("items")->fetchAll();

// returns the username & email of all buyers
$buyers = $db->select("buyers", "username, email")->fetchAll();
```

### fetchAll

`fetchAll` is a method that's used together with the `select` method. This method simply returns an array consisting of a lot of objects. It is mostly used when querying multiple rows.

```php
$items = $db->select("items")->fetchAll();
```

Although the query here is `$db->select("items")`, running just this would return nothing. To actually get the result of this query, you'd need to call `execute`, `fetchObj`, `fetchAssoc` or `fetchAll`.

### execute

This method is used on queries which don't return anything like insert, update and delete queries. This method just runs the desired query and returns `null`, however, if there is a problem, it returns `false`. You can then call `$db->errors()` to get the exact error.

### fetchObj

This is just like `fetchAll` except that fetchObj is used on select queries usually involving one row

```php
$db->select("users")->where("id", "1")->fetchObj();
```

If `fetchAll` is used in this case, the result would look something like this:

```php
[
  [
    "id" => "1"
  ]
]
```

Also, note that `fetchObj` returns an object, so you can use the result like this

```php
$user = $db->select("users")->where("id", "1")->fetchObj();
$user->id // not $user["id"]
```

### fetchAssoc

This is just like the `fetchObj` method, except that it returns an associative array, not an object.

```php
$user = $db->select("users")->where("id", "1")->fetchAssoc();
$user["id"]; // not $user->id
```

### 📩 insert

`Insert` provides a much simpler syntax for making insert queries.

```php
$db->insert("users") // faster than $db->query("INSERT INTO users")
```

### params

This method is used on `insert` and `update` just like how `where` is used on `select` and `delete`.

```php
$db->insert("users")->params("username", "mychi");
```

To actually run this query, you have to call `execute`.

```php
$db->insert("users")->params("username", "mychi")->execute();
```

This inserts a user with a username of mychi into the users table. But what if you wanted to add more params, simple!

```php
$db->insert("users")->params([
  "username" => "mychi",
  "email" => "mickdd22@gmail.com"
])->execute();
```

You're free to arrange this query anyhow you see fit, it's still considered as a single chain.

```php
$db->insert("users")
   ->params([
     "username" => "mychi",
     "email" => "mickdd22@gmail.com",
     "password" => md5("test")
   ])
   ->execute();
```

What if you already registered someone with the username mychi, this tiny flaw could break your authentication system. That's where `unique` comes in🧐

### 🤞 unique

Just as the name implies, `unique` helps prevent duplicates in your database, fun fact, just chain one more method for this functionality🤗

```php
$db->insert("users")
   ->params([
     "username" => "mychi",
     "email" => "mickdd22@gmail.com",
     "password" => md5("test")
   ])
   ->unique("username", "email")
   ->execute();
```

If you have a 100 unique values, don't feel shy, just line them all up.

```php
->unique("username", "email", "what-not", ...)
```

Alternatively, you could just pack a truck load full of uniques in an array

```php
->unique(["username", "email", "what-not", ...])
```

### 📅 update

Quickly write an update query.

```php
$db->update("users")->params("location", "Ghana")->where("id", "1")->execute();
```

This is generally how an update looks like. Just like with insert, you can add up uniques to make sure you don't have duplicates in your database.

### ❌ delete

Let's jump straight in for an example.

```php
$db->delete("users")->execute();// careful now🙂
```

This code above, ladies and gentlemen, will wipe all your users resulting in 7 digit loses🤞

```php
$db->delete("users")->where("id", "1")->execute();
```

You have succesfully deleted user 1

### 🌾 Extras

At this point, there's still a whole lot you can do with Leaf Db.

There are times when you have to insert data you don't know about. What happens if your user enters unsupported info. To fix this, you'll have to run a bunch of checks to find out what kind of information is being saved, but what if you could validate data before saving without writing any extensive validation? Well...prepare to be amazed🧐

#### ⚖ validate

Validate makes sure that correct information is saved in your database. You simply need to chain the `validate` method.

```php
$db->insert("users")
   ->params([
     "username" => "mychi",
     "email" => "mickdd22@gmail.com",
     "password" => md5("test")
   ])
   ->validate("username", "validUsername")
   ->execute();
```

Validate takes in 2 parameters, a field to validate and a validation rule. You can find all the validation rules and what they do [here](2.2-beta/core/forms?id=multiple-rule-validation). So what if you need to validate more than 1 parameter?

```php
$db->insert("users")
   ->params([
     "username" => "mychi",
     "email" => "mickdd22@gmail.com",
     "password" => md5("test")
   ])
   ->validate([
     "username" => "validUsername",
     "email" => "email"
   ])
   ->execute();
```

Amazing right?!

#### 👻 hidden

Not all information which is retrieved from the database is sent over to the client side or is added to the session or cookies. Usually, some fields are left out for "security" reasons. `hidden` returns the retrieved data without the `hidden` fields.

```php
$db->select("users")->hidden("remember_token", "reset_q_id")->fetchAll();
```

```php
$db->select("users")->where("id", "1")->hidden("remember_token", "reset_q_id")->fetchObj();
```

#### ➕ add

That's right, just imagine doing the opposite of `hidden`, instead of hiding fields from the query data, `add` lets you add your own fields into the query data.

```php
$db->select("users")->add("tx_id", gID())->fetchAll();
```

This query adds a `tx_id` field with a value generated from `gID` to every user

```php
$db->select("users")->where("id", "1")->add("tx_id", "d362d7t2366")->fetchObj();
```

This is similar as the query above, except that this query is on the scale of a single user.

#### bind

We've already seen `bind` in action, but we've not actually talked about it. This method allows you to bind parameters into your query.

```php
$db->select("users WHERE username = ?")->bind("mychi")->fetchAssoc();
```

And yet again another syntax🧐 As said above, Leaf  Db is highly customizable, and allows you to write queries in a way that suits you. This statement above binds `mychi` to the username. There's also a second parameter which you really won't be using: the type of parameter.

```php
$db->select("users WHERE username = ?")->bind("mychi", "s")->fetchAssoc();
```

The `s` for the second parameter shows that the parameter you're binding to the username is a string.

```php
$db->select("users WHERE username = ?")->bind(["mychi" => "s"])->fetchAssoc();
```

You can also pass in an array with multiple values.

#### 🚦 limit

When retrieving data from your database for use in applications, you might want to show only a specific number of values.

```php
$itemsPerPage = 15;
$items = $db->select("items")->limit($itemsPerPage)->fetchAll();
```

### 👎 error handling

Errors come up all the time, user errors, that is. What happens when validation fails, or if someone has already registered a username. Leaf Db provides a simple way to track these errors.

```php
$res = $db->insert("users")->params("username", "mychi")->unique("username")->execute();
if ($res === false) $app->response->throwErr($db->errors());
```

Using `$db->errors()` returns an array holding any errors which caused the query to fail. eg:

```php
[
  "email" => "email already exists",
  "username" => "username can only contain characters 0-9, A-z and _
]
```

<br>

[Auth](2.2-beta/core/auth)
[Response](2.2-beta/http/response)
[Request](2.2-beta/http/request)
[Session](2.2-beta/http/session)

Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
