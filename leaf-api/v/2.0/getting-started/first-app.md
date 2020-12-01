# Your first Leaf API ✨

Before you go on, Leaf API is powered by [Leaf](/), so we'll recommend getting familiar with [Leaf PHP Framework](/) first. Not to worry, it takes just about 5-10 minutes to completely learn the basics.

Note that all your development is done in the `App` directory. By default, a few demos have been created to give you a quick idea on how Leaf API works.

## Introduction 📖

For this "tutorial", we'll be building a simple project to learn about Leaf in general. We’re going to be building a simple API to demonstrate how Leaf API works. We’ll be using models, request, response, controllers, migrations, leaf’s command line tool and a whole lot of other tools provided for us.😎

## Our First API

In the [previous section](/leaf-api/v1.2/?id=Installation), we looked at installation, Leaf API's directory structure and running your project, it's assumed you've already read this section.

Also, we'll be using Leaf's console to generate our files, so, it's recommended that you check out [this section](/leaf-api/v1.2/console/)

Now that that’s out of the way, we can start with our actual development. When we take a look at our `index.php` file, we see that Leaf Core is initialised and a bunch of files including our routes are imported.

As such, `index.php` serves as our project root. Every request/page load passes through `index.php` first and this is done because of the [.htaccess](/2.1/intro/htaccess) file.

### Routing

In v2, the `Routes.php` file has been replaced with the `Routes` directory. If you however want to continue using the `Routes.php`, you can create a `Routes.php` file and link it in the `index.php` file in the root directory.

Example routes have been created to give you a fair idea on how to handle routing with Leaf. You can check out Leaf router's docs [here](/2.1/routing/).

Now, let’s get started.

```php
<?php
$app->get('/', function() {
  // Do something here
});

Route("GET", "/", function() {
  // Do something here
});
```

This is what a basic Leaf route looks like.

But in this case we're working in an MVC environment, we would want controllers to handle various routes, so, let's do just that.

### Using Controllers

The first thing we need to do to use a controller is obviously to create the controller. Our controllers are kept in `App/Controllers`…you can manually create your controller in this directory, but there’s a better way😊. Remember we talked about the Leaf Console? We’re going to generate a controller now using the Leaf console tool. Open up your console and type:

```bash
php leaf g:controller PagesController
```

This will generate a controller in our `App/Controllers` directory

Back in our routes file, we can use this controller like so:

```php
$app->get('/home', '\App\Controllers\PagesController@index');

Route("GET", "/", "\App\Controllers\PagesController@index");
```

That's it. Now, let's look at our controller

```php
<?php

namespace App\Controllers;

class PagesController extends Controller {
  public function index()
  {
    json([
      "key" => "value"
    ]);
  }
}
```

`json` is a new method available in v2. `json` provides the functionality of both `respond` and `respondWithCode` which are both deprecated. Since most APIs output json, `json` is a method you'll be using a lot.

### Request

Response handles the way data goes out of our application, on the flip side, Request handles the data that comes into our application. You can find Leaf Request docs [here](/2.1/http/request).

Let's look at a basic example. Inside our controller:

```php
public function search() {
  $keywords = $this->request->get("keywords");

  // ... handle search operation
  $this->json($results);
}
```

There are however global methods like `json` we saw above. You can use these methods from anywhere within your app. There are also global methods for request as well: `requestData` or `request` and `requestBody`, using global methods, the example above will look like this:

```php
public function search() {
  $keywords = requestData("keywords");

  // ... handle search operation
  json($results);
}
```

### Models & Migrations

Our models represent our data layer, usually from a database. Our models are kept in the `App/Models` directory. Controllers get required information from models which is then passed into the response. We won't be doing much work in the model itself, since all the ground work has already been done by Leaf Core.

***To use your database, you have to head to `.env` and configure your database: set the databse name, username, password...***

In v2, after configuring your .env variables, if the database doesn't exist, you can create it with Leaf console`

```bash
php leaf db:install
```

Now, let's generate a model.

```bash
php leaf g:model Post
```

This will generate a simple model.

If we don't have a `posts` table, we can create a migration along with the model. Migrations help us create database tables right off the bat without writing long SQL.

```bash
php leaf g:model Post -m
```

After this, you should find a new migration in `App\Database\Migrations` looking like `YYYY_MM_DD_TIME_create_posts.php`. So, in this file, we can create all the rows we want inside our table.

```php
<?php
namespace App\Database\Migrations;

use Leaf\Database;

class CreateUsers extends Database {
  public function __construct() {
    parent::__construct();
  }
  
  /**
   * Run the migrations.
   *
   * @return void
   */
  public function up()  {
    if(!$this->capsule::schema()->hasTable("posts")):
      $this->capsule::schema()->create("posts", function ($table) {
        $table->increments('id');
        $table->string('author_id');
        $table->string('title');
        $table->text('body');
        $table->timestamps();
      });
    endif;
  }
  
  /**
    * Reverse the migrations.
    *
    * @return void
    */
  public function down() {
    $this->capsule::schema()->dropIfExists("posts");
  }
}
```

After that, we can run our migrations from the console with:

```bash
php leaf db:migrate
```

So now we can work with the table we generated. Let's look at our model. You can read more on [Leaf Models](/2.1/core/model)

```php
<?php
namespace App\Models;

class Post extends Model {
  //
}
```

### Using our model

As mentioned before, we don't really do much in the model. The magic happens in our controller. Let's generate a new controller.

```bash
php leaf g:controller PostsController --resource
```

We added the resource flag to it in order to generate a `resource controller`.

When we look in `App/Controllers/PostsController`, we see:

```php
<?php
namespace App\Controllers;

class PostsController extends Controller {
  /**
   * Display a listing of the resource.
   */
  public function index() {
    //
  }

  /**
   * Show the form for creating a new resource.
   */
  public function create() {
    //
  }

  /**
   * Store a newly created resource in storage.
   */
  public function store() {
    //
  }

  /**
   * Display the specified resource.
   */
  public function show($id) {
    //
  }

  /**
   * Show the form for editing the specified resource.
   */
  public function edit($id) {
    //
  }

  /**
   * Update the specified resource in storage.
   */
  public function update($id) {
    //
  }

  /**
   * Remove the specified resource from storage.
   */
  public function destroy($id) {
    //
  }
}
```

A resource controller is filled with resource methods which quickly help us perform CRUD functions.

So let's say we have a database named `blog` with a table named `posts` which has some data in it, to retrieve all the data in the `posts` table, we'll head to our controller. The first thing we'll have to do is to bring in our `Post` model. This will allow us to use our database.

```php
<?php
namespace App\Controllers;

// our model
use App\Models\Post;

class PostsController extends Controller {
  public function __construct() {
    .....
```

Now let's head over to our index method and enter this:

```php
public function index() {
  json(Post::all());
}
```

`Post::all()` is a method which will query our database and retrieve all our `posts` for us, we're using `json()` to send all our posts to a client as JSON.

All that's left now is to add a route for our controller. In our `App\Routes` directory:

```php
$app->setNamespace('\App\Controllers');

$app->get('/', 'PagesController@index');
$app->resource('/posts', 'PostsController');
```

So when we navigate to `/posts` in our browser, we see all our posts in JSON format.

For a blog app, we'd usually want to see our latest posts first, so we can order the posts by the time they were created. In our controller,

```php
public function index() {
  json(Post::orderBy('id', 'desc')->get());
}
```

This will get the latest posts first.

Next, we'll want to show a particular post when we navigate to `/post/{id}` eg: when we go to `/posts/2` in our browser, we would want to see the post 2...so, in our controller's show method, we simply have to get that particular post and pass it into the response. We can get the current post with `Post::find($id);`

```php
public function show($id) {
  json(Post::find($id));
}
```

Here are a bunch of other cool stuff you can do wiith the model in our controller,

```php
// find a post by title
Post::where('title', 'Post Two')->get();

// create a new post
$post = new Post;
$post->title = requestData("title");
$post->body = requestData("body");
$post->save();

// delete a post
$post = Post::find($id);
$post->delete();
```

## Next Steps

- [Routing](/leaf-api/v1.2/core/routing)
- [Leaf Console](/leaf-api/v1.2/utils/console)
- [Helper Functions](/leaf-api/v1.2/utils/functions)
- [Controllers](/leaf-api/v1.2/core/controllers)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
