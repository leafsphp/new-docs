# Leaf UI: Custom Elements <sup class="new-tag-1">New</sup>

Custom elements for Leaf UI are pre-created elements which combine a set of features from regular markup. They make it a lot easier to perform some UI tasks.

One distinguishing feature is that all custom elements start with `_`. Also, although they're named custom elements, they are parsed into valid HTML and CSS in the browser. Let's look at the supported custom elements.

## Style

This is a custom element which provides a simpler a simpler way to use stylesheets in your Leaf UI. `Style` unlike [`createStyles`](ui/v/0.1.0/core?id=createstyles) allows you to also import external styles.

It takes in 2 parameters:

- (string|array) The styles to use. Pass in an array to use styles directly and a string for an external stylesheet

- (array, optional) Attributes

```php
// external style import
Style("./style.css");

// "in UI" styles
Style([
  "body" => "background-color: #fcfcfc;"
]);

// "in UI" styles with attributes
Style([
  "body" => "background-color: #fcfcfc;"
], ["type" => "text/css"]);

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
```

## Script

This works pretty much the same way `Style` works. It allows you to scripts inside your Leaf UI.

It takes in 2 parameters:

- (string|array) The scripts to use. Pass in an array to use scripts directly and a string for an external script

- (array, optional) Attributes

```php
// external script import
Script("./main.js");

// "in UI" script - Note that array must contain a string
Script(["
  alert('This is an alert');
"]);
```

### Uppercase

Makes all takes uppercase. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
Uppercase("This is uppercase");
```

### Lowercase

Makes all text lowercase. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
Lowercase("This is a lowercase");
```

## Container

Container is an element inspired by bootstrap's `.container`. It pretty much creates a container around an object. It takes in 2 parameters:

- (array, optional) Container attributes eg: style, ...

- (array) Children

```php
Container([], [
  // children here
]);
```

## Row

Row just as the name indicates, creates a row. It works using CSS Flexbox and therefore creates a flex row. It takes in 2 parameters:

- (array, optional) Row attributes eg: style, ...

- (array) Children

```php
$ui::Row([], [
  // children here
]);
```

## Column

This custom element creates a flex column. It takes in 2 parameters:

- (array, optional) Column attributes eg: style, ...

- (array) Children

```php
$ui::Column([], [
  // children here
]);
```

## Creating your own elements (Components)

As far as PHP is concerned, all Leaf UI elements are just PHP functions, with this in mind, simply create a function and return a Leaf UI. That's it! There's no need to extend classes and all that when everything is already available for you.

```php
function MyButton($children, $props)
{
  return button(div(["class" => "btn-content-wrapper"], $children), array_merge(
    $props, ["class" => "custom-btn"]
  ));
}

// ...

echo MyButton("click me!", ["color" => "red"]);
```

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
