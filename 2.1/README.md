# 📚 Getting Started

## Leaf PHP v2.1

Leaf v2.1 is the latest release of Leaf PHP Framework that comes along with a bunch of new features, better functionality and fixes from the previous version.

## 📁 Installation

You can view installation for Leaf v2.1 [here](2.1/intro/)

## What's New

### 📑Leaf Db <sup><small style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2.1</small></sup>

Leaf Db is a new lightweight but powerful query builder which allows you quickly write dynamic queries, validate and seperate data in just a single line of code.

```js
$db = new Leaf\Db;
$db->auto_connect();

$user = $db->select("users")
   ->where("username", $username)
   ->validate("username", "validUsername")
   ->hidden("password")
   ->fetchObj()
```

[Read Leaf Db Docs](2.1/db/)

### 🛫Cors Bypass

Just a little handy tool especially useful when building APIs. CORS errors are a very common thing for developers who work with APIs, and this method is just a basic bypass for these errors.

```js
$app = new Leaf\App();
$app->response->cors();

// your code...

$app->run();
```

[Read Response Docs](2.1/http/response)

<br>
<hr>

<a href="#/2.1/intro/htaccess" style="margin: 0px;">Re-routing to index</a>
<a href="#/2.1/intro/first" style="margin: 0px 10px;">Building your first leaf app</a>
<a href="#/2.1/routing/" style="margin: 0px 10px;">Routing</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
