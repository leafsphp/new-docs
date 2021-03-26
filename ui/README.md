# Leaf UI <sup class="new-tag-1">New</sup>

Leaf UI is a simple UI library for PHP. Leaf UI lets you quickly scaffold webpages without leaving the comfort of PHP; No more writing weird strings, no more weird formatting for HTML inside PHP. One thing to note is that all Leaf UI elements render plain HTML in the browser.

## Simple Example

```php
use Leaf\UI;

$ui = form("method", "action", [
  h2("Subscribe to my newsletter"),
  input("type", "name", ["placeholder" => "Enter your email", "label" => "Email"]),
  button("Get Started", ["type" => "submit"])
]);

UI::render($ui);
```

**OUTPUT:**
<div style="padding: 20px;">
  <form method="method" action="action">
    <h2>Subscribe to my newsletter</h2>
    <label for="21es56">Email</label>
    <input id="21es56" type="type" name="name" placeholder="Enter your email">
    <button type="submit">Get Started</button>
  </form>
</div>

As you've noticed, Leaf UI uses a "function based" syntax, as opposed to traditional HTML tags. This syntax is heavily inspired by [flutter](https://flutter.dev) and [reactjs](//reactjs.org)(without JSX).

## Installation

You can install Leaf UI with composer. Simply run:

```bash
composer require leafs/ui
```

<br>

## Next Steps

- [Your first leaf ui](ui/v/0.1.0/first)
- [Basic Usage](ui/v/0.1.0/basic-usage)
- [Custom Elements](ui/v/0.1.0/custom-elements)
- [Creating Custom Elements](ui/v/0.1.0/custom-elements?id=creating-your-own-elements)

<br>

We need your help developing Leaf UI. You can [contribute to Leaf UI on github](https://github.com/leafsphp/leaf-ui/v/0.1.0/)

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
