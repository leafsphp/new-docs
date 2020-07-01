# LeafAPI

Leaf API is a lightweight PHP MVC framework for rapid API development. LeafAPI serves as minimal MVC wrapper around Leaf PHP Framework which allows you to use Leaf in an MVC environment. With a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant APIs.

## Installation

The main installation method for Leaf API is with [composer](https://getcomposer.org).

```bash
composer create-project leafs/api <project-name>
```

This will create a new Leaf API project named `<project-name>`. Inside the new directory, you should have a structure like this.

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

- [First App](/leaf-api/first-app/)
- [Routing](/leaf-api/routing/)
- [Leaf Console](/leaf-api/console/)
- [Controllers](/leaf-api/controllers/)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)