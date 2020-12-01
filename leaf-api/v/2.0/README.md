# Leaf API v2.0

Leaf API is a lightweight PHP MVC framework for rapid API development. Leaf API serves a minimal MVC wrapper around Leaf PHP which basically provides a more scalable and powerful setup. With a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant APIs.

[What's new in v2](leaf-api/v/2.0/new)

## Installation

### Composer

You can quickly create a Leaf API project with [composer](https://getcomposer.org).

```bash
composer create-project leafs/api <project-name>
```

### Leaf CLI <sup class="new-tag-1">NEW</sup>

Leaf CLI is a console tool for creating and managing Leaf projects. Read the guide [here](/cli)

```bash
leaf create <project-name> --api
```

### Directory Structure

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
│   ├───Routes
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

- [First App](/leaf-api/v1.2/getting-started/first-app)
- [Routing](/leaf-api/v1.2/core/routing)
- [Leaf Console](/leaf-api/v1.2/utils/console)
- [Controllers](/leaf-api/v1.2/core/controllers)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)