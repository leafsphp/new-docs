# Leaf 2.3 (Lucky Charm🍀)

## 🙏 Thank YOU

Before you go on, we just want to thank you for all your support with Leaf and it's packages. Lucky Charm is a version filled with goodies and suggestions from you. This is our gift to you😎😎

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

$app = new Leaf\App;

$app->set404();
$app->db->connect("host", "username", "password", "dbname");

$app->get('/book/{id}', function($id) use($app) {
  $app->response->respond([
    "book" => $app->db->select("books")->where("id", $id)->fetchAssoc()
  ]);
});

$leaf->run();
```

## ✨ Quickly Create PHP Projects

Leaf is a PHP framework that helps you create clean, simple but powerful web apps and APIs quickly and easily. Leaf introduces a cleaner and much simpler structure to the PHP language while maintaining it's flexibility. With a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant web apps and APIs.

<br>

## 📂 Installation

#### 💻 Install with composer
You can quickly get leaf installed in your application using composer. Simply run:

```bash
composer require leafs/leaf
```

You can then import leaf into your project and start building all your amazing projects. You can view your project using:

```bash
php -S localhost:8080
```

#### 🎮 New project with Leaf CLI

Leaf CLI is a console tool for creating and managing Leaf projects. Read the guide [here](/cli)

```bash
leaf create <project-name>
```

### 📅 Working with MVC

Although leaf on it's own isn't an MVC framework, it contains useful tools and packages which allow you to use Leaf as any other MVC framework.

If however, you want an already built MVC setup with scaffolding and a whole lot of other amazing features, you can try out [Leaf API](/leaf-api) or [Leaf MVC](//leafmvc.netlify.app).

You can also try out [**Skeleton**](//github.com/leafsphp/skeleton) which provides an easy to use, customizable structure for your Leaf apps. Skeleton gives you some advantages of full blown frameworks like Leaf MVC without the restrictions it comes with.

#### 📄 Leaf API

Leaf API is a lightweight PHP MVC framework for rapid API development. LeafAPI serves as minimal MVC wrapper around Leaf PHP Framework which allows you to use Leaf in an MVC environment. It also comes along with a bunch of handy tools which can speed up your development by leagues🙂

**[Read the docs](/leaf-api/)**
**Contribute to [Leaf API](https://github.com/leafsphp/leafAPI).**

#### 📕 Leaf MVC

Leaf MVC provides an MVC wrapper around Leaf itself. So you can use all of Leaf's cool features alongside a nice set of development tools offered by Leaf MVC.

Although Leaf MVC is useable, there's still a lot of work to be done on it. You can also help with it's development.

**Checkout [Leaf MVC](//leafmvc.netlify.app).**

#### 😎 Leaf UI

Leaf UI is a php framework for building user interfaces😅. As weird as this sounds, this is another project being actively developed.

Leaf UI allows you to focus almost entirely on writing your php application. Instead of having to build interfaces with html, with weird formatting and string interpolations everywhere, Leaf UI gives you a PHP replacement.

Not only does it allow you skip annoying HTML, but also with integrations like [wynter](https://github.com/leafsphp/leaf-ui/tree/wynter), you can write fully-powered Leaf UI apps without touching HTML, CSS or JavaScript. Amazing, right?

```php
$ui = new Leaf\UI\Template;

$users = [
  ["name" => "User 1"],
  ["name" => "User 2"],
  ["name" => "User 3"]
];

$html = $ui::_template("Page Title", [
  $ui::_container([
    $ui::_row([
      $ui::loop($users, function($user) use($ui) {
        return $ui::div(["style" => "background: #fcfcfd;"], [
          $ui::h3($user["name"])
        ]);
      })
    ])
  ])
]);

$ui::render($html);
```

**[Read the docs](ui/)**

As amazing as Leaf UI is, it's still under development and has a whole lot of work left to be done. [Contribute to the Leaf UI project on github.](https://github.com/leafsphp/leaf-ui)

<br>
<hr>

<a href="#/lucky-charm/intro/first" style="margin-right: 10px;">Building your first leaf app</a>
<a href="#/lucky-charm/routing/" style="margin: 0px 10px;">Routing</a>
<a href="#/lucky-charm/core/controller" style="margin: 0px 10px;">Controllers</a>
<a href="#/lucky-charm/core/model" style="margin: 0px 10px;">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
