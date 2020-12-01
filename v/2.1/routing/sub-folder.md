# 📂 Sub-folder support

## 📖 Overview

Out-of-the box Leaf's Core router will run in any (sub)folder you place it into … no adjustments to your code are needed. You can freely move your entry script index.php around, and the router will automatically adapt itself to work relatively from the current folder's path by mounting all routes onto that basePath.

Say you have a server hosting the domain www.example.org using public_html/ as its document root, with this little entry script index.php:

```php
$leaf->get('/', function() { echo 'Index'; });
$leaf->get('/hello', function() { echo 'Hello!'; });
```

- If your were to place this file (along with its accompanying .htaccess file or the like) at the document root level (e.g. public_html/index.php), Leaf's Core router will mount all routes onto the domain root (e.g. /) and thus respond to [https://www.example.org/](https://www.example.org/) and [https://www.example.org/hello](https://www.example.org/hello).

- If you were to move this file (along with its accompanying .htaccess file or the like) into a subfolder (e.g. public_html/demo/index.php), Leaf's Core router will mount all routes onto the current path (e.g. /demo) and thus repsond to [https://www.example.org/demo](https://www.example.org/demo) and [https://www.example.org/demo/hello](https://www.example.org/demo/hello). There's no need for `$leaf->mount(…)` in this case.

## Disabling subfolder support

In case you don't want Leaf's Core router to automatically adapt itself to the folder its being placed in, it's possible to manually override the basePath by calling `setBasePath()`. This is necessary in the (uncommon) situation where your entry script and your entry URLs are not tightly coupled (e.g. when the entry script is placed into a subfolder that does not need be part of the URLs it responds to)..

```php
// Override auto base path detection
$leaf->setBasePath('/');

$leaf->get('/', function() { echo 'Index'; });
$leaf->get('/hello', function() { echo 'Hello!'; });

$leaf->run();
```

If you were to place this file into a subfolder (e.g. public_html/some/sub/folder/index.php), it will still mount the routes onto the domain root (e.g. /) and thus respond to [https://www.example.org/](https://www.example.org/) and [https://www.example.org/hello](https://www.example.org/hello) (given that your .htaccess file – placed at the document root level – rewrites requests to it)

<br>
<hr>

<a href="#/v/2.1/http/request" style="margin: 0px">Request</a>
<a href="#/v/2.1/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/v/2.1/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/2.1/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.1/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>