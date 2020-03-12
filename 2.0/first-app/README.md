# Building your first LeafMVC app
Note that all your development is done in the `app` directory. By default, a few demos have been created to give you a quick idea on how LeafMVC works.


## Introduction
For this "tutorial", we'll be building a simple project to learn about Leaf in general. We’re going to be building a simple blog to demonstrate how LeafMVC works. We’ll be using models, views, controllers, migrations, leaf’s command line tool and a whole lot of other tools provided for us.😎

**NB**
If you want to generate an application from the finished blog, you can run
```bash
composer create-project leafs/mvc <AppName> --prefer-dist dev-blog
```
This will create the blog application for you, so you simply have to link your database and run
```bash
php leaf db:seed
```
That's all, simple right?😂🙌

In the [previous section](/?id=leafmvc), we looked at installation, LeafMVC's directory structure and a basic usage example, it's assumed you've already read this section.

Also, we'll be using Leaf's console to generate our files, so, it's recommended that you check out [this section](/cmd/)

Now that that’s out of the way, we can start with our actual development. When we take a look at our index.php file, we see that Leaf Core is initialised and our route config is also initialised.


LeafMVC’s route config seperates routes into 2 categories: web routes and API routes. All routes which start with `/api` are considered as API routes by route config and are handled in `app/routes/api.php` all other routes are handled in `app/routes/web.php` in the case of this article, all routes will be handled in `app/routes/web.php️` 🤷‍♂️


We’ll be handling our routing in the web.php file. As mentioned before, LeafMVC runs on Leaf Core, routing and a whole lot of other cool features come directly from Leaf Core, so don’t forget to check out [Leaf PHP Framework](https://leaf-docs.netlify.com)🤞. 

Now, let’s get started.

```javascript
<?php
$leaf->get('/', function() {
	// Do something here
});
```
So we can return json encoded data for APIs, html and php pages, raw text......

**See [routing docs](/routing/) for more on routing**

But in this case we're workinh in an MVC environment, we would want controllers to handle various routes, so, let's do just that.

The first thing we need to do to use a controller is obviously to create the controller. Our controllers are kept in `app/controllers` …you can manually create your controller in this directory, but there’s a better way😊. Remember we talked about the Leaf Console? We’re going to generate a controller now using the Leaf console tool. Open up your console and type:
```bash
php leaf g:controller PagesController
```
This will generate a controller in our `app/controllers` directory


Back in our `app/routes/web.php` file, we can use this controller like so:
```javascript
$leaf->get('/home', '\App\Controllers\PagesController@index');
```
That's it. Now, let's look at our controller

```javascript
<?php
namespace App\Controllers;
use Leaf\Controller;

class PagesController extends Controller {
	public function index() {
		$this->set([
			"title" => "Leaf Vein Integration"
		]);
		$this->render("index");
	}
}
```
By default, LeafMVC's controllers are set-up to use Leaf's templating engine(Veins). Veins are very flexible and easy to use, making them a good choice for LeafMVC. You can quickly get this to work by running
```bash
php leaf g:template index
```

This will generate a new Vein, `index.vein` in `app/views`. Just reload your app to see the new vein. With this, we have set up a view and a controller. One major use of MVC(VC) is to be able to pass data to the view from the controller. Let's see how that works in LeafMVC.

Let's go back to our controller. Let's say we have a new variable(object) which contains user info
```javascript
$user = (object) [
	'name' => 'Jane Doe',
	'email' => 'janedoe@gmail.com',
	'logged' => true
];
```
and we want to pass this into our View, we can do this simply with by passing this variable through Leaf Core's already defined `set()`, let's see how that works.

```javascript
public function index() {
	$user = (object) [
		'name' => 'Jane Doe',
		'email' => 'janedoe@gmail.com',
		'verified' => true
	];
	$this->set($user);
	$this->render("index");
}
```
With this, we are passing the user object into our Vein Template. You can read more on Vein Templating [here](/templating/).

Now, open up `app/views/index.vein.php` you're to see this
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
 <title>{function="env('APP_NAME')"}</title>
 <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <link rel="stylesheet" href="/app/views/assets/css/bootstrap.min.css">
</head>
<body>
 <h2>Hi {$user->name}</h2>
 <script src="/app/views/assets/js/jquery.min.js"></script>
 <script src="/app/views/assets/js/bootstrap.min.js"></script>
</body>
</html>
```

To use a variable passed into Veins, we use `{$variable}`, since we passed in the user object, we can use it's components here: eg `{$name}`. Lets see how that works.


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
 <title>{function="env('APP_NAME')"}</title>
 <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <link rel="stylesheet" href="/app/views/assets/css/bootstrap.min.css">
</head>
<body>
	{if="$user->verified"}
		<p>User is verified</p>
	{else}
		<p>User is not verified</p>
	{/if}
	<h2>{$user->name}</h2>
	<p>{$user->email}</p>
	<script src="/app/views/assets/js/jquery.min.js"></script>
	<script src="/app/views/assets/js/bootstrap.min.js"></script>
</body>
</html>
```
Now, we've looked at our View and our Controller. Let's talk about Models. Our models are kept in the `app/models` directory. Models usually handle data: work with databases, data storage...Controllers get required information from models which is then passed to the view. We won't be doing much work in the model itself, since all the ground work has already been done by Leaf Core. Let's first generate a model.
```bash
php leaf g:model Post
```
This will generate a simple model


If we want to add a migration to the model, we can run
```bash
php leaf g:model Post -m
```

```javascript
<?php
    namespace App\Models;

    use Leaf\Database;
    new Database();

    use Leaf\Model;

    class Post extends Model {
        /**
        * The attributes that are mass assignable.
        *
        * @var array
        */
        protected $fillable = [

        ];
    }
```
### IMPORTANT
Now, we'll have to generate a controller to handle our `posts`, we'll name this `PostsController`
```bash
php leaf g:controller PostsController --resource
```
We added the resource flag to it in order to generate a resource controller.

When we look in `app/controllers/PostsController`, we see:
```javascript
<?php

namespace App\Controllers;

use Leaf\Controller;
use Leaf\Http\Request;

class PostsController extends Controller {
    public function __construct() {
        parent::__construct();
        $this->request = new Request;
    }
    
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

***To use your database, you have to head to `.env` and configure your database: set the databse name, username, password...***
So let's say we have a database named `blog` with a table named `posts` which has some data in it, to retrieve all the data in the `posts` table, we'll head to our controller. The first thing we'll have to do is to bring in our `Post` model. This will allow us to use our database.
```javascript
<?php

namespace App\Controllers;

use Leaf\Controller;
use Leaf\Http\Request;

// our model
use App\Models\Post;

class PostsController extends Controller {
    public function __construct() {
		.....
```

Now let's head over to our index method and enter this:
```javascript
public function index() {
	$this->set([
		"posts" => Post::all()
	]);
	$this->render("pages/posts");
```
`Post::all()` is a method which will query our database and retrieve all our posts for us, we're using `$this->set()` to pass that data into our view and `$this->render()` to render the view. In this case we're trying to render `app/views/pages/posts.vein.php`, but it doesn't yet exist, so let's generate it.

```bash
php leaf g:template pages/posts
```

So we can open up our new template and add:
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>{function="env('APP_NAME')"}</title>
	<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
	<link rel="stylesheet" href="/app/views/assets/css/bootstrap.min.css">
</head>
<body>
	{include="../components/header"}

	<div class="container">
		<h2>All Posts</h2>
		{if="count($posts) > 0"}
			{loop="$posts" as $post}
				<div style="margin-bottom: 50px;">
					<h3><a href="/posts/{$post->id}">{$post->title}</a></h3>
					<p>{$post->body}</p>
					<small>Written on {$post->created_at}</small>
				</div>
			{/loop}
		{else}
			There are no posts
		{/if}
	</div>
	<script src="/app/views/assets/js/jquery.min.js"></script>
	<script src="/app/views/assets/js/bootstrap.min.js"></script>
</body>
</html>
```
This is supposed to output all the posts from the database, but one thing's missing: we don't have a route to view all the posts we output. So we head back to our `app/routes/web.php` and add:
```javascript
$leaf->setNamespace('\App\Controllers');

$leaf->get('/', 'PagesController@index');

$leaf->get('/posts', 'PostsController@index');
```
So when we navigate to `/posts` in our browser, we see all our posts


For a blog app, we'd usually want to see our latest posts first, so we can order the posts by the time they were created. In our controller,
```javascript
public function index() {
	$this->set([
		"posts" => Post::orderBy('created_at', 'desc')->get()
	]);
	$this->render("pages/posts");
```
This will get the latest posts first.


Next, we'll want to show a particular post when we click on the post title, to do this, we'll create a new template `post.vein.php`
```bash
php leaf g:template pages/post
```

We'll then render this in our show function in the PostsController
```javascript
public function show($id) {
    $this->render("pages/post");
}
```
Note that show() takes in an id, this id is the id of the post we want to show. This id will come from our route: `posts/id`. So, we need to set up a route for this.
```javascript
$leaf->setNamespace('\App\Controllers');

$leaf->get('/', 'PagesController@index');

$leaf->get('/posts', 'PostsController@index');
$leaf->get('/posts/{id}', 'PostsController@show');
```

When we go to /posts/2 in our browser, we see the template we created before....but we'll want to actually see the post...so, in our controller's show method, we simply have to get that particular post and pass it into the view. We can get the current post with `Post::find($id);`
```javascript
public function show($id) {
    $this->set([
        "post" => Post::find($id)
    ]);
    $this->render("pages/post");
}
```

Then, we can render this in our template
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
 <title>{function="env('APP_NAME')"}</title>
 <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <link rel="stylesheet" href="/app/views/assets/css/bootstrap.min.css">
</head>
<body>
	<h2>{$post.title}</h2>
	<p>
        {autoescape="off"}
            {$post.body}
        {/autoescape}
    </p>
	<script src="/app/views/assets/js/jquery.min.js"></script>
	<script src="/app/views/assets/js/bootstrap.min.js"></script>
</body>
</html>
```
In our controller,
```javascript
// find a post by title
Post::where('title', 'Post Two')->get();

// create a new post
$post = new Post;
$post->title = $this->request->getParam("title");
$post->body = $this->request->getParam("body");
$post->save();

// delete a post
$post = Post::find($id);
$post->delete();
```
<br>
<br>

# <a href="#/cmd/">Leaf CMD</a>
# <a href="#/routing/">Routing</a>
# <a href="#/controllers/">Controllers</a>
# <a href="#/models/">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>