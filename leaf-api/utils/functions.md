# Leaf API Helper Functions 🏥

These are simple-to-use functions that are available everywhere in your application. You can call these functions in your routes, controllers and everywhere you need them.

## Available Functions

### App

This method returns the base Leaf instance. You can perform whatever operation you need on the `App` method.

```php
App()->response->respond(...);
App()->resource("/home", "HomeController");
```

### render

This outputs a blade view.

```php
function user() {
  render("user", ["username" => "Mychi"]);
}
```

### respond

Outputs a JSON encoded response.

```php
$data = ["name" => "BMW", "data" => ["id" => "1", "driver" => "Mychi"]];
respond($data);
```

### Route

This method creates a new route. It takes in 3 parameters:

- The route method(s)
- The route
- The handler

```php
Route("GET|POST", "/me", function() {...});
```

### View

`View` returns a blade view.

```php
$output = View("user", ["username" => "Mychi"]);
```

## Next Steps

- [Routing](/leaf-api/core/routing)
- [Controllers](/leaf-api/core/controllers)
- [Models](/leaf-api/core/models)
- [Migrations](/leaf-api/core/migrations)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
