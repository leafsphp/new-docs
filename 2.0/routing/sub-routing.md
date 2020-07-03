# Sub-routing
Use `$leaf->mount($baseroute, $fn)` to mount a collection of routes onto a subroute pattern. The subroute pattern is prefixed onto all following routes defined in the scope. e.g. Mounting a callback $fn onto /movies will prefix /movies onto all following routes.

```php
$leaf->mount('/movies', function() use ($leaf) {
	// will result in '/movies/'
	$leaf->get('/', function() {
		echo 'movies overview';
	});

	// will result in '/movies/id'
	$leaf->get('/(\d+)', function($id) {
		echo 'movie id ' . htmlentities($id);
	});
});
```

Nesting of subroutes is possible, just define a second `$leaf->mount()` in the callback function that's already contained within a preceding `$leaf->mount()`. Also, Note that nested subroutes currently don't support dynamic url patterns, so, you can only do something like this.

```php
$leaf->mount('/user', function() use ($leaf) {
    $leaf->get('/', function() use($leaf) {
        echo $leaf->response->renderMarkup('no user id');
    });
    $leaf->get('/(\d+)', function($id) use($leaf) {
        echo $leaf->response->renderMarkup("user $id");
    });
    $leaf->mount('/settings', function() use ($leaf) {
        $leaf->get('/privacy', function() use($leaf) {
            echo $leaf->response->renderMarkup('Privacy Settings');
        });
        $leaf->get('/notification', function() use($leaf) {
            echo $leaf->response->renderMarkup("Notification Settings");
        });
    });
});
```

<br>
<hr>

<a href="#/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>