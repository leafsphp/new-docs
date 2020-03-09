# Re-routing to index
## Explanation
Basically, we're trying to push all the requests made to the server to a single root file, so a request made to `/home.php` will be directed to the root file of our choice....usually `index.php`.

This complex sounding feature can be achieved by simply adding a `.htaccess` file to the root of our project directory.

## The HTACCESS file
This is a basic example of an htaccess file. It basically re-routes all requests to our index.php file.
```htaccess
RewriteEngine on
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule . index.php [L]
```
Save as `.htaccess` in your the same directory as your "root file"

<br>
<hr>

<a href="#/2.0/intro/first" style="margin: 0px;">Your first leaf app</a>
<a href="#/2.0/routing" style="margin: 0px 10px;">Routing</a>
<a href="#/2.0/http/request" style="margin: 0px 10px;">Request</a>
<a href="#/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.0/database/intro" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>