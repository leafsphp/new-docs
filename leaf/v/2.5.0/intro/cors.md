<!-- markdownlint-disable no-inline-html -->
# Cors

When working with frontends, you usually come across very annoying CORS errors. For this, Leaf has prepared already configured methods which allow you to solve all your issues with one line of code.

## evade cors

After initializing your Leaf app, you can call `evadeCors` on your app.

It takes in 3 parameters:

- Boolean determining whether to evade options requests. When set to `true`, preflight options requests will return a 200 response. For most apps, this won't cause any problems, however, if it interferes with other requests, you can simply set this to `false` and rely on a 3rd party solution.

***There'll be a complete fix for this targetting only preflight requests in one of the next versions.***

- string containing the allowed origins, default is `*`

- string containing the allowed headers, defaul is `*`

```php
$app = new Leaf\App;

$app->evadeCors(true);

$app->evadeCors(false, "*", "*");

$app->evadeCors(true, "https://example.com", "*");

$app->evadeCors(true, "https://example.com", "X-My-Custom-Header, X-Another-Custom-Header");
```

## cors on response

Another way to deal with cors in Leaf is to use Leaf\Http\Response. The Leaf response object also comes with a `cors` method which allows you to set origins and headers which are allowed. It takes in paramters:

- string containing the allowed origins, default is `*`

- string containing the allowed headers, defaul is `*`

```php
$response->cors();
$response->cors("https://example.com", "X-My-Custom-Header, X-Another-Custom-Header");
$response->cors("https://example.com", "*");
```

## Directly setting access control headers

Leaf headers also provides a helper to quickly set access control headers.

```php
Headers::accessControl([
    "Allow-Origin" => "*", "Allow-Headers" => "*"
]);

// or

Headers::accessControl("Allow-Origin", "https://example.com", 200);
// the final parameter is the status code to send
```

## Next Steps

- [MDN Cors docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- [MDN Cors Headers docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#the_http_response_headers)
- [Routing](leaf/v/2.5.0/routing/)

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
