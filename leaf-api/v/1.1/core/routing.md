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
<<<<<<< HEAD
- [Controllers](/leaf-api/v1.1/core/controllers)
- [Models](/leaf-api/v1.1/core/models)
- [Migrations](/leaf-api/v1.1/core/migrations)
=======
<<<<<<< HEAD:leaf-api/v/1.2/core/routing.md
- [Controllers](/leaf-api/v1.2/core/controllers)
- [Models](/leaf-api/v1.2/core/models)
- [Migrations](/leaf-api/v1.2/core/migrations)
=======
- [Controllers](/leaf-api/v/1.1/core/controllers)
- [Models](/leaf-api/v/1.1/core/models)
- [Migrations](/leaf-api/v/1.1/core/migrations)
>>>>>>> c4444eff90e57ffbe2066a11c61ad5d686b48693:leaf-api/v/1.1/core/routing.md
>>>>>>> c4444eff90e57ffbe2066a11c61ad5d686b48693

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
