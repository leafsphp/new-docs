# Your first Leaf API ✨

Before you go on, Leaf API is powered by [Leaf](/), so we'll recommend getting familiar with [Leaf PHP Framework](/) first. Not to worry, it takes just about 5-10 minutes to completely learn the basics.

Note that all your development is done in the `App` directory. By default, a few demos have been created to give you a quick idea on how Leaf API works.

## Introduction 📖

For this "tutorial", we'll be building a simple project to learn about Leaf in general. We’re going to be building a simple API to demonstrate how Leaf API works. We’ll be using models, request, response, controllers, migrations, leaf’s command line tool and a whole lot of other tools provided for us.😎

<!-- **NB**
If you want to generate an application from the finished blog, you can run
```bash
composer create-project leafs/mvc < AppName > --prefer-dist dev-blog
```
This will create the blog application for you, so you simply have to link your database and run
```bash
php leaf db:seed
```
That's all, simple right?😂🙌 -->

## Our First API

In the [previous section](/leaf-api/?id=Installation), we looked at installation, Leaf API's directory structure and running your project, it's assumed you've already read this section.

Also, we'll be using Leaf's console to generate our files, so, it's recommended that you check out [this section](/leaf-api/console/)

Now that that’s out of the way, we can start with our actual development. When we take a look at our `index.php` file, we see that Leaf Core is initialised and a bunch of files including our routes are imported.

As such, `index.php` serves as our project root. Every request/page load passes through `index.php` first and this is done because of the [.htaccess](/2.1/intro/htaccess) file.

<!-- Leaf API’s route config seperates routes into 2 categories: web routes and API routes. All routes which start with `/api` are considered as API routes by route config and are handled in `app/routes/api.php` all other routes are handled in `app/routes/web.php` in the case of this article, all routes will be handled in `app/routes/web.php️` 🤷‍♂️ -->

### Routing

In Leaf API, all our routes are defined in `App/Routes.php`. You can check out Leaf router's docs [here](/2.1/routing/).

Now, let’s get started.

```javascript
<?php
$app->get('/', function() {
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

Back in our `App/Routes.php` file, we can use this controller like so:

```js
$app->get('/home', '\App\Controllers\PagesController@index');
```

That's it. Now, let's look at our controller

```js
<?php
namespace App\Controllers;

class PagesController extends Controller {
  public function index() {
    $this->render("index", [
      "title" => "Leaf Blade Integration"
    ]);
  }
}
```

### Templating

By default, Leaf API's controllers are set-up to use Leaf Blade. Leaf Blade is Leaf's adaptation of the laravel blade engine(originally forked from [https://github.com/jenssegers/blade/](https://github.com/jenssegers/blade/)). Blade is flexible, popular and easy to use, making it a good choice for Leaf API. You can quickly get this to work by running

```bash
php leaf g:template index
```

This will generate a new template `index.blade.php` in `App/Views`. This view is simply just to introduce you to views, but we won't be using this in our API. We can delete this unused template:

```bash
php leaf d:template index
```

### Response

Let's go back to our controller. Since this is an API, we'll want to output some sort of data to a client as a response. We can easily do this with [Leaf Response](/2.1/http/response). Note that `Response` is directly bound to the controller, so you can use all response methods on `$this`

```js
public function index() {
  $this->respond("Output over here");
}
```

### Request

Response handles the way data goes out of our application, on the flip side, Request handles the data that comes into our application. You can find Leaf Request docs [here](/2.1/http/request)

Let's look at a basic example. Inside our controller:

```js
public function search() {
  $keywords = $this->request->get("keywords");

  // ... handle search operation
  $this->respond($results);
}
```

### Models & Migrations

Our models represent our data layer, usually from a database. Our models are kept in the `App/Models` directory. Controllers get required information from models which is then passed into the response. We won't be doing much work in the model itself, since all the ground work has already been done by Leaf Core.

***To use your database, you have to head to `.env` and configure your database: set the databse name, username, password...***

Let's first generate a model.

```bash
php leaf g:model Post
```

This will generate a simple model.

If we don't have a `posts` table, we can create a migration along with the model. Migrations help us create database tables right off the bat without writing long SQL.

```bash
php leaf g:model Post -m
```

After this, you should find a new migration in `App\Database\Migrations` looking like `YYYY_MM_DD_TIME_create_posts.php`. So, in this file, we can create all the rows we want inside our table.

```js
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

```javascript
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

```js
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

```js
<?php
namespace App\Controllers;

// our model
use App\Models\Post;

class PostsController extends Controller {
  public function __construct() {
    .....
```

Now let's head over to our index method and enter this:

```js
public function index() {
  $this->respond(Post::all());
}
```

`Post::all()` is a method which will query our database and retrieve all our `posts` for us, we're using `$this->respond()` to send all our posts to a client as JSON.

All that's left now is to add a route for our controller. In `App\Routes.php`:

```js
$app->setNamespace('\App\Controllers');

$app->get('/', 'PagesController@index');
$app->resource('/posts', 'PostsController');
```

So when we navigate to `/posts` in our browser, we see all our posts in JSON format.

For a blog app, we'd usually want to see our latest posts first, so we can order the posts by the time they were created. In our controller,

```js
public function index() {
  $this->respond(Post::orderBy('id', 'desc')->get());
}
```

This will get the latest posts first.

Next, we'll want to show a particular post when we navigate to `/post/{id}` eg: when we go to `/posts/2` in our browser, we would want to see the post 2...so, in our controller's show method, we simply have to get that particular post and pass it into the response. We can get the current post with `Post::find($id);`

```javascript
public function show($id) {
  $this->respond(Post::find($id));
}
```

Here are a bunch of other cool stuff you can do wiith the model in our controller,

```js
// find a post by title
Post::where('title', 'Post Two')->get();

// create a new post
$post = new Post;
$post->title = $this->request->get("title");
$post->body = $this->request->get("body");
$post->save();

// delete a post
$post = Post::find($id);
$post->delete();
```

## Next Steps

- [Routing](/leaf-api/core/routing)
- [Leaf Console](/leaf-api/utils/console)
- [Controllers](/leaf-api/core/controllers)
- [Models](/leaf-api/core/models)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
