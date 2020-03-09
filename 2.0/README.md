# Leaf

Leaf is a PHP framework that helps you create clean, simple but powerful web apps and APIs quickly. Leaf introduces a cleaner and much simpler structure to the PHP language while maintaining it's flexibility. With a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant web apps and APIs. 

# Getting Started
## Installation
With LeafMVC, you can whip up a full MVC app in a couple of seconds. Leaf MVC's recommended mode of installation is with [composer](https://getcomposer.org).
```bash
composer create-project leafs/mvc <project-name>
```
This will create a LeafMVC project and install all dependencies. Also, a `.env` file will be created for you.
You can serve your project with 
```bash
php leaf serve
```

## Folder Structure
```bash
C:.
├───app
│   ├───console
│   ├───controllers
│   │   └───Auth
│   ├───database
│   │   ├───factories
│   │   ├───migrations
│   │   └───seeds
│   ├───helpers
│   ├───models
│   ├───routes
│   └───views
│       ├───assets
│       │   ├───css
│       │   ├───images
│       │   └───js
│       ├───components
│       └───pages
│           └───errors
├───config
├───public
├───storage
│   ├───app
│   │   └───public
│   ├───framework
│   │   └───views
│   └───logs
└───vendor
```
In LeafMVC, ***app*** is where all your development goes on. “app” contains all your **models**, **views**(templates), **controllers**, **routes**, **custom console commands**, **helpers** and database related stuff(**migrations**, **seeds…**).


***config*** contains all the app configurations…configuration for routes, database, the leaf console, error handling, session, templating…however, you normally have no business with this folder


***public*** holds web configuration😅😅.


***storage*** holds all the app data, it contains both framework data and user files. For instance, uploaded files and pictures are kept in storage/app/public


***vendor*** holds all of leafMVC’s dependencies


## Basic Usage
LeafMVC is created with Leaf Core, hence, you can still use the Leaf Code you're used to.<br>
`app/routes/routes.php`
```javascript
<?php
$leaf->get('/home', function() use($response) {
  $response->respond(['Message' => 'Hello World']);
});
```
Just enter this code and run `php leaf serve` and navigate to localhost:3000
It's that simple to build with LeafMVC

<br>
<br>

# <a href="#/first-app/">Building your first leaf app</a>
# <a href="#/cmd/">Leaf CMD</a>
# <a href="#/routing/">Routing</a>
# <a href="#/controllers/">Controllers</a>
# <a href="#/models/">Models</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>