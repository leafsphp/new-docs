# Routing
All Leaf MVC's routes are kept in `app/routes`. Leaf MVC uses Leaf Core's router for it's routing. This means that it's the same as Leaf's routing. You can check it out [here](https://leaf-docs.netlify.com/v1.4.2/routing/simple-routing.html). 


LeafMVC has 2 route files, `web.php` and `api.php`. Routes are divided into web routes and API routes by the route config: all routes which begin with /api are considered API routes and a handled by `app/routes/api.php`, all others are handled in the `web.php` file.


# Sample Routes
```javascript
// get request
$leaf->get('/user/{id}', function($id) {
	$response->respond([
		"mesage" => "Your id is $id"
	]);
});

// using controllers
$leaf->get('/user/{id}', 'Class@method');
```

Read [Leaf Routing Docs](https://leaf-docs.netlify.com/v1.4.2/routing/simple-routing.html).
<br>
<br>

# <a href="#/cmd/">Leaf CMD</a>
# <a href="#/veins/">Veins</a>
# <a href="#/controllers/">Controllers</a>
# <a href="#/models/">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>