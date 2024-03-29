# 📚 Getting Started

## What is Leaf

Leaf is a PHP framework that helps you create clean, simple but powerful web apps and APIs quickly. Leaf introduces a cleaner and much simpler structure to the PHP language while maintaining it's flexibility.

With a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant web apps and APIs.

Simply install Leaf, and you're good to go.

## 📁 Installation

Leaf's has a very simple installation method. You can install directly with composer or clone our repo on github. (both methods require composer)

### Install with composer

Composer is a dependency manager for PHP, just like npm for javascript and ruby gems. Therefore, you need to have PHP installed on your system. If you don't already have composer installed, you can download it [here](https://getcomposer.org/)

After downloading composer, you can run this command to install leaf in your project folder.

```bash
composer require leafs/leaf
```

### 🎮 New project with Leaf CLI <sup class="new-tag-1">NEW</sup>

Leaf CLI is a console tool for creating and managing Leaf projects. Read the guide [here](https://cli.leafphp.dev)

```bash
leaf create <project-name>
```

<!-- ### Install with Github

Download from github and run `composer install` to get all dependencies

```bash
git clone --single-branch --branch 2.x https://github.com/leafsphp/leaf.git
```

OR

<div style="border: 1px solid rgba(10, 230, 150, 0.8); border-radius: 4px; background: rgba(10, 230, 150, 0.05); padding: 20px 30px; padding-bottom: 32px;">
	<div style="font-weight: bolder; font-size: 25px; margin-bottom: -18px !important;">Setup</div>
	<p style="color: rgb(5, 160, 70); font-size: 18px;">
		You can directly clone or download the git repo here.
	</p>
	<a href="https://github.com/leafsphp/leaf/" style="background: #202020; color: white; text-decoration: none; padding: 8px 15px; border-radius: 3px;">Download Repo</a>
</div> -->

### 🚀 Build with Leaf API

You can also try out our [LeafAPI](/leaf-api/) package. This is another framework built around the `Leaf` package. Leaf API provides you with tools to quickly and efficiently build an API. Leaf APIis built with what we call MRRC(Model Request Response Controller) architecture which is pretty much MVC without the V. It also has scaffolding, a custom terminal, migrations, an ORM and other cool features.

```bash
composer create-project leafs/api <project-name>
```

or

```bash
leaf create <project-name> --api
```

### 🚀 Build with Leaf MVC

You can also try out our [LeafMVC](https://leafmvc.netlify.app) package. This is a simple yet powerful MVC framework wrapped around the `Leaf` package which helps you build with Leaf in an MVC setup. It comes with a custom terminal, scafffolding, migrations, an ORM and many more features. You can install it with this command.

```bash
composer create-project leafs/mvc <project-name>
```

or

```bash
leaf create <project-name> --mvc
```

<br>
<hr>

<a href="#/leaf/v/lucky-charm/intro/htaccess" style="margin: 0px;">Re-routing to index</a>
<a href="#/leaf/v/lucky-charm/intro/first" style="margin: 0px 10px;">Building your first leaf app</a>
<a href="#/leaf/v/lucky-charm/routing/" style="margin: 0px 10px;">Routing</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>