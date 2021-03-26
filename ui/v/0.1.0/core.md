# Core Concepts

There are a couple of methods which serve as Leaf UI's core: The most important being `createElement`.

## createElement

This method simply allows you to create(render) a native HTML element.

It takes in 3 parameters:

- HTML Element To Render eg: h2 (string, required)

- Element props (including children). You can use an empty array if there are no attributes (array, optional). If you have only one child, you can pass in a string instead of a whole array with the `children` prop.

- Element type: (optional) This refers to the HTML tag type. Leaf UI supports 3 types:

  - `UI::SINGLE_TAG` for a single tag eg: `meta` and HTML 5 input (`<element attributes>`)

  - `UI::SELF_CLOSING` for a self closing tag `<element attributes />`

  - If the value is not one of the above or this field is left blank, a normal HTML is created `<element attributes>children</element>`

```php
UI::createElement("h2", ["id" => "title"], type);
```

## createStyles

Create styles simply allows you to write styles in your Leaf UI, pretty much like how `<style>` lets you write styles in HTML.

It takes in 2 parameters:

- The styles you want to apply (array)

- Attributes for your style tag when Leaf UI renders in the browser. Leave blank or an empty array if there are no attributes (array)

```php
// no attributes/ class selector
UI::createStyles([
  ".home" => "background: #fefefe;"
], []);

// no attributes/element selector
UI::createStyles([
  "h2" => "font-family: sans-serif;"
]);

// renders <style type="text/css">
UI::createStyles([
  "#btn" => "padding: 10px 15px;"
], ["type" => "text/css"]);

// media query example
UI::createStyles([
  "@media only screen and (max-width: 500px)" => [
    "p > button#btn" => "border: 1px solid grey;"
  ]
])
```

Checkout [a simpler alternative to this](ui/v/0.1.0/custom-elements?id=style)

## loop

This is an element created to handle loops in your Leaf UI. Since your entire Leaf UI is just a function👌, you can't use "mult-line functions" like `foreach`, `for`, `if`..., therefore, this method has been prepared. It takes in 2 parameters:

- The array to loop through
- A callable handler for loop

The callable should return an element

```php
$users = [
  ["name" => "user 1", "rank" => "D"],
  ["name" => "user 2", "rank" => "F"],
  ["name" => "user 3", "rank" => "S"],
];
// ...
Row([
  UI::loop($users, function($user) use(UI) {
    return Column([
      h2($user["name"]),
      small($user["rank"])
    ]);
  })
])
```

Also, you can access both the key and value of an array during the loop.

```php
$user = ["name" => "user 1", "rank" => "D"];

Column([
  UI::loop($user, function($value, $key) use(UI) {
    return Row([
      span("$key:"),
      h4($value)
    ]);
  })
])
```

## randomId

This method as the name suggests, generates a random id. Under the hood Leaf UI uses this method to generate an id for any element which isn't given an id. It takes in 1 param:

- A string to add to id, usually an element name (optional)

```php
UI::randomId("div");
```

## Render

This method allows you to output the UI you've created into the browser.

```php
$html = UI::body([...]);
UI::render($html);

// or
UI::render(UI::body([...]));
```
