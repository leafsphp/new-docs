# Leaf UI: Custom Elements <sup style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2.1 alpha</sup>

Custom elements for Leaf UI are pre-created elements which combine a set of features from regular markup. They make it a lot easier to perform some UI tasks.

One distinguishing feature is that all custom elements start with `_`. Also, although they're named custom elements, they are parsed into valid HTML and CSS in the browser. Let's look at the supported custom elements.

## _style

This is a custom element which provides a simpler a simpler way to use stylesheets in your Leaf UI. `_style` unlike [`create_styles`](ui/?id=create_styles) allows you to also import external styles.

It takes in 2 parameters:

- (string|array) The styles to use. Pass in an array to use styles directly and a string for an external stylesheet

- (array, optional) Attributes

```php
// external style import
$ui::_style("./style.css");

// "in UI" styles
$ui::_style([
	"body" => "background-color: #fcfcfc;"
]);

// "in UI" styles with attributes
$ui::_style([
	"body" => "background-color: #fcfcfc;"
], ["type" => "text/css"]);
```

## _script

This works pretty much the same way `_style` works. It allows you to scripts inside your Leaf UI.

It takes in 2 parameters:

- (string|array) The scripts to use. Pass in an array to use scripts directly and a string for an external script

- (array, optional) Attributes

```php
// external script import
$ui::_script("./main.js");

// "in UI" script - Note that array must contain a string
$ui::_script(["
	alert('This is an alert');
"]);
```

### _uppercase

Makes all takes uppercase. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
$ui::_uppercase("This is uppercase");
```

### _lowercase

Makes all text lowercase. It takes in 2 parameters:

- (string|array) Child/Children
- (array, optional) Attributes

```php
$ui::_lowercase("This is a lowercase");
```

## _container

Container is an element inspired by bootstrap's `.container`. It pretty much creates a container around an object. It takes in 2 parameters:

- (array, optional) Container attributes eg: style, ...

- (array) Children

```php
$ui::_container([], [
	// children here
]);
```

## _row

Row just as the name indicates, creates a row. It works using CSS Flexbox and therefore creates a flex row. It takes in 2 parameters:

- (array, optional) Row attributes eg: style, ...

- (array) Children

```php
$ui::_row([], [
	// children here
]);
```

## _column

This custom element creates a flex column. It takes in 2 parameters:

- (array, optional) Column attributes eg: style, ...

- (array) Children

```php
$ui::_column([], [
	// children here
]);
```

## Creating your own elements

For now, these are the only "completed/working" custom elements. But that's not all, you can also create your own custom components.

The first method is used when you want to create a new class. This method presents more control over your components. It also allows you to overwrite already built components, though that's not adviced.

The second is an experimental feature which allows you to create custom components without starting a new instance of Leaf UI.

### 1: Extending Leaf UI

As mentioned before, with this method, you'd need to create a new class which extends Leaf UI. From there you can create methods which contain your custom components.

**Note that your custom elements should render valid HTML, CSS or Javascript.**

**It is recommended that your custom components names start with `_`**

```php
// creating components
class MyUI extends Leaf\UI {
	public static function _shadowBox($children, $props = []) {
		return self::div([
			"style" => "box-shadow: 1px 0px 4px #fafafa; padding: 10px 8px;",
		], $children);
	}
}

// using components
$html = MyUI::_shadowBox([
	MyUI::p("Nothing strange is happening here")
]);

// rendering components
MyUI::render($html);
```

### 2: make()

This method allows you to create custom elements on the current instance of Leaf UI. It takes in 2 parameters:

- (string) The element name. **just a tip:** The custom element naming convention is to start with `_`

- (callable) The handler to create the element

```php
$ui::make("_avatar", function() {
    $avatar = [];
    $avatar["style"] = "border-radius: 50%; border: 1px solid black; width: 50px; height: 50px";
    $avatar["props"] = ["src" => "./img.jpg", "alt" => "xxx"];
    $avatar["compile"] = "img";
    return $avatar;
});
```

As you see in this example, the callable/call-back function should return an array (for now, we really don't want this🤦‍♀️😪).

As mentioned earlier, custom components return HTML (CSS/JS), as such, you are to specify the native element you want your custom element to return. You can do this with the `compile` selector on your array.

```php
$ui::make("_avatar", function() {
    return ["compile" => "img"];
});
```

But simply returning a native HTML element doesn't make your component any different from the original element. This is where your styles come in. Using the `style` selector in the array, you can use any CSS you want.

```php
$ui::make("_avatar", function() {
    return [
		"compile" => "img",
		"style" => "border-radius: 50%; border: 1px solid black; width: 50px; height: 50px"
	];
});
```

Finally, you can set some default attributes/props for your compiled HTML tag defined in `compile`. We do this using `props`.

```php
$ui::make("_avatar", function() {
    return [
		"compile" => "img",
		"style" => "border-radius: 50%; border: 1px solid black; width: 50px; height: 50px",
		"props" => ["src" => "./img.jpg", "alt" => "xxx"]
	];
});
```

To use this custom defined component `_avatar`, you need to call the `custom` method.

### custom

Custom is a method that allows you use custom defined components defined with `make`. It takes in 4 parameters:

- (string) The element you want to call
- (array, optional) The element props/attributes
- (array, optional) Children
- (string, optional) Tag type, UI::SELF_CLOSING, UI::SINGLE_TAG.

```php
$ui::custom("_avatar", ["alt" => "User img"], [], $ui::SINGLE_TAG);
```

<br>
<hr>

<a href="#/ui/basic-usage" style="margin: 0px">Basic Usage</a>
<a href="#/ui/custom-elements" style="margin: 0px 10px;">Custom Elements</a>
<a href="#/2.1-alpha/views/blade" style="margin: 0px; 10px;">Blade Templating</a>
<a href="#/2.1-alpha/http/session" style="margin: 0px 10px;">Session</a>
<a href="#/2.1-alpha/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>