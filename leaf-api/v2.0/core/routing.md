# Routing

All Leaf API's routes are kept in `App/Routes.php`. Leaf API uses Leaf Core's router for it's routing. This means that it's the same as Leaf's routing. You can check it out [here](/2.1/routing/).

## Sample Routes

```php
// get request
$app->get('/user/{id}', function($id) {
  respond([
    "mesage" => "Your id is $id"
  ]);
});

// using controllers
$app->get('/user/{id}', 'Class@method');

Route("GET", "/users", "Class@method");
```

## Next Steps

- [Leaf Core Routing](/2.1/routing/)
- [Controllers](/leaf-api/v1.2/core/controllers)
- [Models](/leaf-api/v1.2/core/models)
- [Migrations](/leaf-api/v1.2/core/migrations)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
