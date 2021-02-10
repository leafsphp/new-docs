# 📚 Getting Started

## Leaf PHP: v2.4.2 (🥬 Desert Wishbone-bush)

Just like the previous beta, v2.4.2 looks to build up on existing features, and improves their usage by providing compatability upgrades as well as new methods which compliment use cases of those features. As such, all new features still center around existing implementations. Note that changes from this release will also be shipped in later versions of [LeafMVC](/), [LeafAPI](/) and [Skeleton](/).

## 📁 Installation

You can install leaf quickly using composer.

```bash
composer require leafs/leaf
```

This command can also be run in your LeafMVC and LeafAPI projects to manually update leaf.

## 💡 What's New

Building a better experience for existing features doesn't necessarily mean that there's nothing new in Leaf. To view all the changes made to Leaf since the last release, you can check the [release notes](https://github.com/leafsphp/leaf/releases/tag/v2.4.1). However, the major additions include:

- Added option to turn off experimental method warnings

- Added `Form::rule` which allows you to create your own rules for form validation.

```php
Form::rule("max", function($field, $value, $params) {
    if (strlen($value) > $params) {
        Form::addError($field, "$field can't be more than $params characters");
        return false;
    }
});
```

- Added internal `Leaf\Form` feature which allows you to pass parameters to validation rules.

```php
$validation = Form::validate([
    // To pass a param to a rule, just use :
    "username" => "max:3",
]);
```

- Added `Form::addError` which allows you to add errors to be returned in `Form::errors()`

```php
Form::addError($field, "$field can't be more than $params characters");
```

- Added max and min rules by default

```php
$validation = Form::validate([
    "username" => "max:1",
    "password" => "min:81",
]);
```

- Guards can be used even in API mode. This will alert you if you're not eligible to view a particular page.

Read the [release notes](https://github.com/leafsphp/leaf/releases/tag/v2.4.2) to view all changes.

**Note that the release notes are still being updated.**

<br>
<hr>

## Next steps

- [Intro](leaf/v/2.4.2/intro/)
- [Configuring .htaccess](leaf/v/2.4.2/intro/htaccess)
- [Your first leaf app](leaf/v/2.4.2/intro/first)
- [Routing](leaf/v/2.4.2/routing/)

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
