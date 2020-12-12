# Default Views (Templating) <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span></sup>

Currently, Leaf has support for 3 templating engines, **Leaf Views**, **Leaf Veins** and **Leaf Blade:** Leaf's implementation of **Laravel Blade**. Here, we'll be looking at Leaf Views.

## Intro

To directly access Leaf Views, you have to initialise the `Leaf\View` class, however, just like with some other core features, Leaf Views have been bound to the `Leaf` object, so you can call it directly without initialising it seperately.

You can use the Leaf application’s` render()` method to ask the current view object to render a template with a given set of variables. The Leaf application’s` render()` method will echo() the output returned from the view object to be captured by an output buffer and appended automatically to the response object’s body. This assumes nothing about how the template is rendered; that is delegated to the view object.

```php
$leaf->get('/books/:id', function ($id) use ($leaf) {
    $leaf->render('view.php', ['id' => $id]);
});
```

If you need to pass data from the route callback into the view object, you must explicitly do so by passing an array as the second argument of the Leaf application’s `render()` method like this:

```php
$leaf->render('view.php', ['id' => $id]);
```

You can also set the HTTP response status when you render a template:

```php
$leaf->render('500.php', ['id' => $id], 500);
```

#### Example Template
```php
<p>This is user number <?php echo $id; ?></p>
```

<hr>

## Creating your Custom Views

A Leaf application delegates rendering of templates to its view object. A custom view is a subclass of `\Leaf\View` that implements this interface:

```php
public render(string $template);
```

The view object’s `render` method must return the rendered content of the template specified by its `$template` argument. When the custom view’s render method is invoked, it is passed the desired template pathname (relative to the Leaf application’s “templates.path” setting) as its argument. Here’s an example custom view:

```php
<?php
class CustomView extends \Leaf\View
{
    public function render($template)
    {
        return 'The final rendered template';
    }
}
```

The custom view can do whatever it wants internally so long as it returns the template’s rendered output as a string. A custom view makes it easy to integrate popular PHP template systems like Twig or Smarty.

**Note that a custom view may access data passed to it by the Leaf application’s render() method with $this->data.**

### Example View

```php
<?php
class CustomView extends \Leaf\View
{
    public function render($template)
    {
        $template === 'show.php'
        $this->data['title'] === 'Sahara'
    }
}
```

### Example Integration

If the custom view is not discoverable by a registered autoloader, it must be required before the Leaf application is instantiated.

```php
<?php
require 'CustomView.php';

$leaf = new \Leaf\Leaf(array(
    'view' => new CustomView()
));

$leaf->get('/books/:id', function ($id) use ($leaf) {
    $leaf->render('show.php', array('name' => 'Michael'));
});

$leaf->run();
```

<hr>

## Handling Templating Data

**You'll not really need to use these methods, as you can easily pass any data through the render method.**

The view object’s `setData()` and `appendData()` methods inject data into the view object; the injected data is available to view templates. View data is stored internally as a key-value array.

#### Setting Data
The view object’s `setData()` instance method will overwrite existing view data. You may use this method to set a single variable to a given value:

```php
$leaf->view->setData('color', 'red');
```

The view’s data will now contain a key “color” with value “red”. You may also use the view’s `setData()` method to batch assign an entire array of data:

```php
$leaf->view->setData([
    'color' => 'red',
    'size' => 'medium'
]);
```

Remember, the view’s `setData()` method will replace all previous data.

#### Appending Data
The view object also has a `appendData()` method that appends data to the view’s existing data. This method accepts an array as its one and only argument:

```php
$leaf->view->appendData([
    'foo' => 'bar'
]);
```

<br>
<hr>

<a href="#/leaf/v/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/leaf/v/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/leaf/v/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/leaf/v/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/leaf/v/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>