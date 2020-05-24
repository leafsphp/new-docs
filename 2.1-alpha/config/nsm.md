# Names and Scopes
When you build a Leaf application you will enter various scopes in your code (e.g. global scope and function scope). You will likely need a reference to your Leaf application in each scope. There are several ways to do this:

- Use application names with the Leaf application’s `getInstance()` static method
- Curry an application instance into function scope with the `use` keyword

<hr>

## Application Names
Every Leaf application may be given a name. **This is optional**. Names help you get a reference to a Leaf application instance in any scope throughout your code. Here is how you set and get an application’s name:

```js
<?php
$leaf = new \Leaf\App();
$leaf->setName('foo');
$name = $leaf->getName(); // "foo"
```

## Scope Resolution
So how do you get a reference to your Leaf application? The example below demonstrates how to obtain a reference to a Leaf application within a route callback function. The `$leaf` variable is used in the global scope to define the HTTP GET route. But the `$leaf` variable is also needed within the route’s callback scope to render a template.

```js
$leaf = new \Leaf\App();

$leaf->get('/foo', function () {
    $leaf->render('foo.php'); // <-- ERROR
});
```
This example fails because the $leaf variable is unavailable inside the route callback function.

### Currying
We can inject the `$leaf` variable into the callback function with the `use` keyword:
```js
$leaf = new \Leaf\App();

$leaf->get('/foo', function () use ($leaf) {
    $leaf->render('foo.php'); // <-- SUCCESS
});
```

<hr>

# Modes
It is common practice to run web applications in a specific mode depending on the current state of the project. If you are developing the application, you will run the application in “development” mode; if you are testing the application, you will run the application in “test” mode; if you launch the application, you will run the application in “production” mode.

Leaf supports the concept of modes in that you may define your own modes and prompt Leaf to prepare itself appropriately for the current mode. For example, you may want to enable debugging in “development” mode but not in “production” mode. The examples below demonstrate how to configure Leaf differently for a given mode.

## What is a mode?
Technically, an application mode is merely a string of text - like “development” or “production” - that has an associated callback function used to prepare the Leaf application appropriately. The application mode may be anything you like: “testing”, “production”, “development”, or even “foo”.

## How do I set the application mode?
### Use an environment variable
If Leaf sees an environment variable named “LEAF_MODE”, it will set the application mode to that variable’s value.
```js
$_ENV['LEAF_MODE'] = 'production';
```

### Use application setting
If an environment variable is not found, Leaf will next look for the mode in the application settings.
```js
$leaf = new \Leaf\App([
    'mode' => 'production'
]);
```

### Default mode
If the environment variable and application setting are not found, Leaf will set the application mode to “development”.

## Configure for a Specific Mode
After you instantiate a Leaf application, you may configure the Leaf application for a specific mode with the Leaf application’s configureMode() method. This method accepts two arguments: the name of the target mode and a callable function to be immediately invoked if the first argument matches the current application mode.

Assume the current application mode is “production”. Only the callable associated with the “production” mode will be invoked. The callable associated with the “development” mode will be ignored until the application mode is changed to “development”.

```js
<?php
// Set the current mode
$leaf = new \Leaf\App([
    'mode' => 'production'
]);

// Only invoked if mode is "production"
$leaf->configureMode('production', function () use ($leaf) {
    $leaf->config([
        'log.enable' => true,
        'debug' => false
	]);
});

// Only invoked if mode is "development"
$leaf->configureMode('development', function () use ($leaf) {
    $leaf->config([
        'log.enable' => false,
        'debug' => true
	]);
});
```

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>