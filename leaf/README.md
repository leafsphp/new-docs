# Leaf PHP

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

$app = new Leaf\App;

$app->set404();
$app->db->autoConnect();

$app->get('/resources', function($id) use($app) {
  $app->response->respond([
    "resource" => $app->db()->select("resources")->all()
  ]);
});

$leaf->run();
```

## ✨ Quickly Create PHP Projects

Leaf is a PHP framework that helps you create clean, simple but powerful web apps and APIs quickly and easily. Leaf introduces a cleaner and much simpler structure to the PHP language while maintaining it's flexibility. With a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant web apps and APIs.

<br>

## 📂 Installation

### 💻 Install with composer

You can quickly get leaf installed in your application using composer. Simply run:

```bash
composer require leafs/leaf
```

You can then import leaf into your project and start building all your amazing projects. You can view your project using:

```bash
php -S localhost:8080
```

### 🎮 New project with Leaf CLI

You may also create a Leaf project using [Leaf CLI](/cli)

```bash
leaf create <project-name>
```

## 🐾 Next Steps

From here, you'll have Leaf installed in your project. You can jummp to one of these pages.

- [Intro](leaf/v/2.4.4/)
- [Your first leaf app](leaf/v/2.4.4/intro/first)
- [Handling Request](leaf/v/2.4.4/http/request)
- [Handling Responses](leaf/v/2.4.4/http/response)

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
