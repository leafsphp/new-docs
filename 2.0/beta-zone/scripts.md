# Leaf JS Scripts <sup><span style="background: rgb(191, 200, 70); color: white; padding: 3px 7px; font-size: 12px;">BETA</span></sup>

This is a funny idea we just sort of made up during development. This whole `Scripts` functionality lets us use some JavaScript methods from our PHP apps without having to write nasty PHP strings with with variables....

To use these scripts, you simply have to call whichever method you need on the `Leaf\JS\Scripts` object, since all of it's methods are static

## Script Methods

### c_log

You might have guessed it😂. That's right, that's our `console.log`. It works exactly like how the javascript console.log works, so there's no need to speak much on this.

```js
Leaf\JS\Scripts::c_log("Text", ["message" => "Arrays are formatted into JSON"]);
```

### localstorage_set

Our version of `localstorage.setItem` works the same way too. Arrays are made json by default.

```js
Leaf\JS\Scripts::localstorage_set("name", "Mychi Darko");
```

### localstorage_get

```js
$name = Leaf\JS\Scripts::localstorage_get("name");
```

### localstorage_remove

```js
Leaf\JS\Scripts::localstorage_remove("name");
```

### localstorage_clear

```js
Leaf\JS\Scripts::clear();
```

<hr>

### [Back to beta zone](2.0/beta-zone/)

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>