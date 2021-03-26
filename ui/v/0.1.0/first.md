# Your First Leaf UI

This is a little "tutorial" that goes through some basic use cases for Leaf UI. After reading to the end, you'll be fully equiped to build your next UI; after all, it's really just HTML :-)

You can install leaf UI with composer:

```sh
composer require leafs/ui
```

After that, we create a new PHP file and initialize leaf UI:

`index.php`

```php
<?php

require __DIR__ . "/vendor/autoload.php";

Leaf\UI::elements();

echo p("Hello world!");
```

Here, we're simply outputting:

```html
<p>Hello world!</p>
```

The line `Leaf\UI::elements()` imports the elements library so we can use shortcut functions like `p()`. Everything from there, is a free-for-all. You can use your HTML elements, styles and scripts as methods.

```php
$html = small("I am really small");
```

You might be wondering how we can use `echo` to output our Leaf UI and even set the output from out functions as variables...well, secret reveal: all Leaf UIs are just strings.

Moving on, let's look at props. We use props to set `class`es `id`s and so much more, depending on the type of element. Leaf UI allows you to pass props into components and elements as an array. Let's look at an example:

```php
div(["class" => "item-list"], [
    h2("Text here"),
]);

small("Text", ["id" => "sm"]);
```

As you can see, some elements take in their `props` before their `children`, others do the opposite. This is because some elements are used more without props: like elements that usually take text in as a `child`.

**`children` is a special property of elements which contains any `child` elements defined within the element, e.g. the `h2` inside the `div` above.**

## Conditional rendering

Conditional rendering is done pretty much the same way as done in JSX: using ternaries. Since we're basically just passing down functions, we can't use `if`, `else` and all those blocks. What we need is a single lined condition:

```php
$gender = "male";

// text example
echo p(
    $gender === "male" ? "I am male" : "I am female"
);

// element example
echo p(
    $gender === "female" ? big("I am female") : small("I am male")
);
```

## Using loops

The fact that multilined blocks won't work with leaf UI means that we can't use `for`, `foreach`, ... So how do we loop through values? Leaf UI has an inbuilt function modeled after array map which allows us to make loops in a single line.

```php
$names = ["Michael", "Mychi", "Darko"];

$html = div(["class" => "name-list"], UI::loop($names, function ($name) {
    return b("$name ");
}));
```

## Adding styles

You can also use CSS with Leaf UI. You can either link an external CSS file or directly type your CSS inside your Leaf UI all using the `Style` tag:

```php
$html = html([
  head([
    title("My app title"),

    // bootstrap CDN
    Style("https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/css/bootstrap.min.css"),

    // local styles
    Style("./style.css"),

    // css in php :-)
    Style([
      "body" => [
        "background" => "grey",
        "font-family" => "sans-serif",
      ],

      // you can also use styles this way
      "p" => "font-size: 20px; font-weight: normal;",

      // you can even use media queries
      "@media only screen and (max-width: 500px)" => [
        "body" => [
          "background" => "silver"
        ],
      ],
    ]),
  ]),
  body([
    p("This is a full scaffold!"),
  ]),
]);

echo $html;
```

You might have noticed that this element begins with an uppercase S. This is because this is a custom element, not one that comes with "html". **Custom element names all begin with uppercase.** This is just a naming convention, not a rule.

## Adding Scripts

Just as you can add styles, scripts can also be added using `Script`, another custom element.

```php
// external [recommended]
Script("./index.js");

// JS in PHP?
Script(["
    var welcome = 'Welcome';

    alert(welcome);
"]);
```

## Next Steps

- [Basic Usage](ui/v/0.1.0/basic-usage)
- [Custom Elements](ui/v/0.1.0/custom-elements)
- [Creating Custom Elements](ui/v/0.1.0/custom-elements?id=creating-your-own-elements)

<br>

We need your help developing Leaf UI. You can [contribute to Leaf UI on github](https://github.com/leafsphp/leaf-ui/v/0.1.0/)

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
