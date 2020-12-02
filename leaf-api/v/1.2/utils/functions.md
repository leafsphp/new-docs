# Leaf API Helper Functions 🏥

These are simple-to-use functions that are available everywhere in your application. You can call these functions in your routes, controllers and everywhere you need them.

## Available Functions

### app

**In v1.2 beta, `App` has been renamed to `app`**

This method returns the base Leaf instance. You can perform whatever operation you need on the `app` method.

```php
app()->response->respond(...);
app()->resource("/home", "HomeController");
```

### d

This method returns the leaf date object. You can use any [Leaf Date](2.1/core/date) method on `d`.

```php
$timestamp = d()->random_timestamp();
```

### dbRow

This method returns a row in a database table. It takes in 3 parameters:

- The table to use
- The row id
- The fields to return (optional, will return all if nothing is specified)

```php
$user = dbRow("users", "1");
$item = dbRow("items", 2, "name, user_id");
```

### fs

This returns the [Leaf FS](2.1/core/fs) object. So you can use all it's methods on `fs`

```php
fs()->create_folder("new_logs");
```

### email

This method allows you to [write an email directly](2.1/core/mail?id=write)

```php
email([
  "subject" => "This is a full Write Test",
  "template" => "./template.html",
  "recepient_email" => "mychi.darko@gmail.com",
  "sender_name" => "Leaf PHP Framework",
  "attachment" => "./../attachment.txt"
]);
```

### markup

Render markup as a response

```php
markup("<h2>Hello</h2>");
```

### plural

This method allows you to get the plural version of a string.

```php
$word = "todo";
plural($word); // returns "todos"
```

### render

This outputs a blade view.

```php
function user() {
  render("user", ["username" => "Mychi"]);
}
```

### requestBody

`requestBody` returns the whole body of a request.

```php
$loginData = requestBody();
$username = $loginData["username"];
```

### requestData

This method returns a particular parameter in the request body

```php
$username = requestData("username");
```

### respond

Outputs a JSON encoded response.

```php
$data = ["name" => "BMW", "data" => ["id" => "1", "driver" => "Mychi"]];
respond($data);
```

### respondWithCode

`respondWithCode` sends JSON encoded data with a code and the appropriate headers as a response

```php
respondWithCode($data, 201);
```

### Route

This method creates a new route. It takes in 3 parameters:

- The route method(s)
- The route
- The handler

```php
Route("GET|POST", "/me", function() {...});
```

### sessionBody

This method returns all session data

```php
$session_data = sessionBody();
```

### sessionGet

Return a session variable

```php
$user = sessionGet("user");
```

### sessionSet

Add a new session variable

```php
$user = sessionSet("user", ["id" => "1"]);
```

### singular

This method allows you to get the singular version of a string.

```php
$word = "todos";
singular($word); // returns "todo"
```

### throwErr

Throws a json encoded error with appropraite headers.

```php
throwErr("user not found", 404);
```

Note that `throwErr` pauses code execution, and so, no code after `throwErr` runs. You can use this with conditional statements for a better effect.

```php
if (!$user->isLoggedIn) throwErr("User not logged in");
```

### view

**In v1.2 beta, `View` has been renamed to `view`**

`view` returns a blade view.

```php
$output = view("user", ["username" => "Mychi"]);
```

## Next Steps

<<<<<<< HEAD:leaf-api/v/1.2/utils/functions.md
- [Routing](/leaf-api/v1.2/core/routing)
- [Controllers](/leaf-api/v1.2/core/controllers)
- [Models](/leaf-api/v1.2/core/models)
- [Migrations](/leaf-api/v1.2/core/migrations)
=======
- [Routing](/leaf-api/v/1.2/core/routing)
- [Controllers](/leaf-api/v/1.2/core/controllers)
- [Models](/leaf-api/v/1.2/core/models)
- [Migrations](/leaf-api/v/1.2/core/migrations)
>>>>>>> c4444eff90e57ffbe2066a11c61ad5d686b48693:leaf-api/v1.2/utils/functions.md

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
