# LeafAPI

<p class="alert -info">
  <b>Leaf MVC v3 (🎻 Stroh)</b> has just been released. "🎻 Stroh" builds on the changes from Leaf PHP and takes API development to a whole new level of ease. <a href="https://api.leafphp.dev">Read the docs</a>
</p>

Leaf API is a lightweight PHP MVC framework for rapid API development. LeafAPI serves as minimal MVC wrapper around Leaf PHP Framework which allows you to use Leaf in an MVC environment. With a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant APIs.

## Installation

### Composer

You can quickly create a Leaf API project with [composer](https://getcomposer.org).

```bash
composer create-project leafs/api <project-name>
```

That's it! This will create a new Leaf API project named `<project-name>`.

### Github

You can [download the source files](https://github.com/leafsphp/leafAPI/archive/v2.0.zip) from github and  extract it to get the LeafAPI files. All that's left is to install the dependencies.

```sh
composer install
```

After this has completed it's installation, you just need to generate your application env file. You can copy and rename your `.env.example` file to `.env`, but aloe cli provides a way easier approach.

```sh
php leaf env:generate
```

That's all!

## Directory Structure

In your project directory, you should have a structure like this.

```bash
C:.
├───App
│   ├───Console
│   ├───Controllers
│   ├───Database
│   │   ├───Factories
│   │   ├───Migrations
│   │   └───Seeds
│   ├───Helpers
│   ├───Models
│   └───Views
├───Config
│   └───Command
├───Lib
├───public
├───storage
│   ├───app
│   │   └───public
│   ├───framework
│   │   └───views
│   └───logs
└───vendor
```

In the project root, you can open up your console tool and type in

```bash
php leaf serve
```

This will start the php web server and load your project at `http://localhost:5500` by default.

## Next Steps

- [First App](/leaf-api/v/2.0/intro/first-app)
- [Routing](/leaf-api/v/2.0/core/routing)
- [Leaf Console](/leaf-api/v/2.0/utils/console)
- [Controllers](/leaf-api/v/2.0/core/controllers)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
