# Inserting Data

Leaf DB has provided really simple, but very helpful methods for inserting data into the database.

<!-- <span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span> -->

## db insert

#### Saving data
We user `$db->insert` to save data in the database. `insert` takes in a "table" to insert data, "column(s)" and "value(s)":

```js
$db->insert("posts", "title", "This is post One");
```

You can also add multiple columns like so:

```js
$db->insert("posts", "title, body", "post One, This is the body of post One");
```

#### Using Prepared Statements
Prepared statements help protect against SQL injection,...

```js
$db->insert("posts", "title, body", "?, ?", ["post One, This is the body of post One"]);
```

<hr>

## Db add <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span></sup>

`add` simply offers a more consice, powerful way to retrieve data from a database. It also uses prepared statements by default, so you're safe in that respect.

Instead of several parameters in `$db->insert`, `$db->add` takes in an array with key-value pairs to be saved in the database.

```js
$db->add("posts", ["title" => "Post One", "body" => "This is the body"]);

// $db->add($table, $params_to_insert);
```


#### Uniques
Let's say you want to check whether the username a user just entered has been taken, you'd have to write a bunch of conditional code, making the code count larger and more error prone, right?

Well, `add` solves this problem smoothly. `add` has a 3rd parameter: an array of unique values which makes sure that the same value can't be saved twice.

```js
$db->add("users", ["name" => "mychi", "email" => "m@m.com", "pass" => "1234"], ["name", "email"]);
```

So, we're telling `add` to alert us if someone has already registered with the name `mychi` or the email `m@m.com`. This is because we passed `["name", "email"]` as the 3rd param to `add`

**With uniques, you can cut down on your whole app:**
For instance, if you know the exact data you'll be receiving in your app, let's say a username, email and password from a register form, you can do something like this:

```js
$leaf->post("/register", function() use($leaf) {
	$leaf->db->add("users", $leaf->request->body(), ["username", "email"]);
});
```

So, we pass in the entire request body, which contains the username, email and password. Simple right?


#### Validation

`add` also has inbuilt validation which validates parameters according to set rules. This uses the [`Leaf\Form->validate`](2.0/form) method. You can check it out for more information on validation.

`add` takes in a 4th parameter which is a boolean, this is whether of not to validate the data passed into `add` using the default checks. 

By default, `add` validates values with the keys: `email`, `username` and any other field is marked as `required`. If any of the validations fail, an error is raised. You can turn this feature off:

```js
$db->add("posts", ["title" => "Post One", "body" => "..."], ["title"], false);
```

#### Custom Validation

This is the 5th parameter of `add`. These are custom rules that you set to validate.

```js
$db->add("posts", ["title" => "Post One", "body" => "..."], ["title"], false, [
	"author" => "validUsername"
]);
```
Here, we're telling `add` that the **author** parameter should be a valid username. If thiscondition(rule) is not met, the application throws an error and breaks.

You can view all validation rules [here](2.0/form?id=validation)

```js
$db->add($table, $params, $uniques, $defaultChecks, $validation);
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
