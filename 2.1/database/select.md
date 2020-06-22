# Retrieving Data

If you're attempting to use this, you've probably seen or used `SELECT` statements before. Leaf DB has provided an even easier way to use select.

Leaf has provided a new method to make retrieving data even simpler and more organised. `choose`

## db select

#### Getting all rows from a table

To do this, we use the `select()` methode. All that we have to do is to pass in the table we want to retrieve. For example, to get all users from the "users" table, we simply do:

```js
$db->select("users");
```

To actually get the results, we'll have to chain `fetchAll()` to the select method. `fetchAll()` does the same thing that `mysqli_fetch_all()` does to an mysqli result

```js
$db->select("users")->fetchAll();
```

#### Getting a column from a table

Getting a single column, eg: getting all usernames from the users table

```js
$db->select("users", "username")->fetchAll();
```

This is like saying `SELECT username FROM users`. You can also pass in multiple options

```js
$db->select("users", "username, email")->fetchAll();
```

You can get all columns with:
```js
$db->select("users")->fetchAll();
//  or
$db->select("users", "*")->fetchAll();
```

#### Getting a particular row from a table

Getting a particular row, eg: getting the user with the id of 1 from the users table. You acan achieve this with:

```js
$db->select("users", "*", "id = 2")->fetchObj();
```

`fetchObj` does the same thing as `mysqli_fetch_obj` and `fetch(PDO::FETCH_OBJ)`

If you don't need the whole row, you can use:

```js
$db->select("users", "username, email", "id = 2")->fetchObj();
```

#### Limit data

Limiting data is also very simple with Leaf DB

```js
// get the latest 10 posts 
$users = $leaf->db->select("posts ORDER BY id DESC LIMIT 10")->fetchAll();

// with parameters
$books = $leaf->db->select("books", "*", "author = ? ORDER BY id DESC LIMIT 5", [$author])->fetchAll();
```

#### Using Prepared Statements

Prepared statements help protect against SQL injection,...

```js
$db->select("users", "*", "username = ? AND password = ?", [$username, $password])->fetchObj();
```

<hr>

## Db choose

`choose` simply offers a more consice, powerful way to retrieve data from a database. It also uses prepared statements by default, so you're safe in that respect.

For basic uses, we'll recommend you use `select`:

```js
$db->select("users")->fetchAll();

$db->select("users", "username")->fetchAll();

$db->select("users", "username, email")->fetchAll();
```

#### Getting a particular row from a table

Getting a particular row, eg: getting the user with the id of 2 from the users table. You acan achieve this with:

```js
$db->choose("users", "*", ["id" => 2])->fetchObj();
```

If you don't need the whole row, you can use:

```js
$db->choose("users", "username, mobile", ["email" => "mickdd22@gmail.com"])->fetchObj();
```

#### Data Options

So unlike `select`, choose takes in an array, which is much clearner than writing partial SQL queries, also, the params you pass in are safe from SQL injection.

Also, unlike select, you seperate data options like `LIMIT` and `ORDER` into a 4th parameter

```js
$db->choose("books", "*", ["author" => "mychi.darko", "published" => "2019"], "LIMIT 5");
```

#### Validation

`choose` also has inbuilt validation which validates parameters according to set rules. This uses the [`Leaf\Form->validate`](2.1/core/form) method. You can check it out for more information on validation.

`choose` takes in a fifth parameter which is a boolean, this is whether of not to validate the data passed into `choose` using the default checks. 

By default, `choose` validates values with the keys: `email`, `username` and any other field is marked as `required`. If any of the validations fail, an error is raised. You can turn this feature off:

```js
$db->choose("books", "*", ["author" => "mychi.darko", "published" => "2019"], "LIMIT 5", false);
```

#### Custom Validation

This is the sixth parameter of `choose`. These are custom rules that you set to validate.

```js
$db->choose("books", "*", ["author" => "mychi.darko", "published" => "2019"], "LIMIT 5", false, [
	"author" => "validUsername",
	"published" => "number"
]);
```

Here, we're telling `choose` that the **author** parameter should be a valid username, and the **published** param should contain only numbers. If any of these conditions(rules) are not met, the application throws an error and breaks.

You can view all validation rules [here](2.1/core/form?id=validation)

```js
$db->choose($table, $fields, $params, $options, $defaultChecks, $validation);
```

<br>
<hr>

<a href="#/2.1/http/request" style="margin: 0px">Request</a>
<a href="#/2.1/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.1/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.1/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.1/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>