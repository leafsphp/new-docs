# 📚 Getting Started

## What is Leaf

Leaf is a PHP framework that helps you create clean, simple but powerful web apps and APIs quickly. Leaf introduces a cleaner and much simpler structure to the PHP language while maintaining it's flexibility.

With a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant web apps and APIs.

To get started, simply install Leaf, and you're good to go.

## 📁 Installation

There are 2 main ways available. Using composer makes everything a lot easier, but if you want more control and customization, you might want to download the source code and setup an autoloader. This way, you can directly edit leaf's files to behave the way you decide.

### Composer installation

Composer is a dependency manager for PHP, just like npm for javascript and ruby gems. Therefore, you need to have PHP installed on your system. If you don't already have composer installed, you can download it [here](https://getcomposer.org/)

After downloading composer, you can run this command to install leaf in your project folder.

```bash
composer require leafs/leaf ^2.5.0-beta
```

### Github clone

You can also clone the repo and setup your autoloader.

<div class="download-alert">
  <h3>Setup</h3>
  <p>
    You can directly download the v2.5.0-beta release here.
  </p>
  <a
    href="https://github.com/leafsphp/leaf/archive/v2.5.0-beta.zip"
    download
  >Download Repo</a>
</div>

**Example autoloader: `autoloader.php`**

```php
<?php
spl_autoload_register(function ($class) {
  $file = str_replace('\\', '/', $class);

  if (!file_exists("leaf/src/$file.php")) return;

  require "leaf/src/$file.php";
});
```

The autoloader will allow you use leaf files without having to `require` or `include` them first. So straight up using `Leaf\Auth` will load `leaf\src\auth.php`.

**This is only required if you downloaded the repo.**

## 🖥 Deploying Leaf Apps

Leaf is created and configured to work right out of the box, even in a production environment. No matter what you use: shared hosting, vps, ... with any web server of your choice, if your app works on localhost, it works in production. This is also true for Leaf MVC, Leaf API and skeleton.

This simply means you can use Leaf for projects of all sizes, no matter the environment it's going to be deployed in.

<br>
<hr>

## Next steps

- [Configuring .htaccess](leaf/v/2.5.0-beta/intro/htaccess)
- [Your first leaf app](leaf/v/2.5.0-beta/intro/first)
- [Routing](leaf/v/2.5.0-beta/routing/)

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
