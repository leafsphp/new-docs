# 🎐 Optional Route Subpatterns

*This guide assumes you have read [Simple Routing](leaf/v/2.1/routing) and [dynamic routing](leaf/v/2.1/routing/dynamic)*

Route subpatterns can be made optional by making the subpatterns optional by adding a ? after them. Think of blog URLs in the form of /blog(/year)(/month)(/day)(/slug):

```php
$leaf->get('/blog(/\d+)?(/\d+)?(/\d+)?(/[a-z0-9_-]+)?', function($year = null, $month = null, $day = null, $slug = null) {
  if (!$year) { echo 'Blog overview'; return; }
  if (!$month) { echo 'Blog year overview'; return; }
  if (!$day) { echo 'Blog month overview'; return; }
  if (!$slug) { echo 'Blog day overview'; return; }
  echo 'Blogpost ' . htmlentities($slug) . ' detail';
});
```

The code snippet above responds to the URLs /blog, /blog/year, /blog/year/month, /blog/year/month/day, and /blog/year/month/day/slug.

**Note**: With optional parameters it is important that the leading / of the subpatterns is put inside the subpattern itself. Don't forget to set default values for the optional parameters.

The code snipped above unfortunately also responds to URLs like /blog/foo and states that the overview needs to be shown - which is incorrect. Optional subpatterns can be made successive by extending the parenthesized subpatterns so that they contain the other optional subpatterns: The pattern should resemble /blog(/year(/month(/day(/slug)))) instead of the previous /blog(/year)(/month)(/day)(/slug):

```php
$leaf->get('/blog(/\d+(/\d+(/\d+(/[a-z0-9_-]+)?)?)?)?', function($year = null, $month = null, $day = null, $slug = null) {
  // ...
});
```

**Note**: It is highly recommended to always define successive optional parameters.

To make things complete use [quantifiers](http://www.php.net/manual/en/regexp.reference.repetition.php) to require the correct amount of numbers in the URL:

```php
$leaf->get('/blog(/\d{4}(/\d{2}(/\d{2}(/[a-z0-9_-]+)?)?)?)?', function($year = null, $month = null, $day = null, $slug = null) {
  // ...
});
```

<br>
<hr>

<a href="#/leaf/v/2.1/http/request" style="margin: 0px">Request</a>
<a href="#/leaf/v/2.1/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/leaf/v/2.1/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/leaf/v/2.1/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/leaf/v/2.1/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>