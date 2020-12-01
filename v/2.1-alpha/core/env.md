# Leaf Environment

## What is the Environment?

A Leaf application’s “environment” is an associative array of settings that are parsed once and made accessible to the Leaf application and its middleware. You are free to modify the environment variables during runtime; changes will propagate immediately throughout the application.

When you instantiate a Leaf application, the environment variables are derived from the `$_SERVER` superglobal; you do not need to set these yourself. However, you are free to modify or supplement these variables in Leaf middleware.

These variables are fundamental to determining how your Leaf application runs: the resource URI, the HTTP method, the HTTP request body, the URL query parameters, error output, and more. Middleware, described later, gives you the power to - among other things - manipulate environment variables before and/or after the Leaf application is run.

## Environment Variables
The following text respectfully borrows the same information originally available at http://rack.rubyforge.org/doc/files/SPEC.html. The environment array must include these variables:


#### REQUEST_METHOD
The HTTP request method. This is required and may never be an empty string.

#### SCRIPT_NAME
The initial portion of the request URI’s “path” that corresponds to the physical directory in which the Leaf application is installed — so that the application knows its virtual “location”. This may be an empty string if the application is installed in the top-level of the public document root directory. This will never have a trailing slash.

#### PATH_INFO
The remaining portion of the request URI’s “path” that determines the “virtual” location of the HTTP request’s target resource within the Leaf application context. This will always have a leading slash; it may or may not have a trailing slash.

#### QUERY_STRING
The part of the HTTP request’s URI after, but not including, the “?”. This is required but may be an empty string.

#### SERVER_NAME
When combined with SCRIPT_NAME and PATH_INFO, this can be used to create a fully qualified URL to an application resource. However, if HTTP_HOST is present, that should be used instead of this. This is required and may never be an empty string.

#### SERVER_PORT
When combined with SCRIPT_NAME and PATH_INFO, this can be used to create a fully qualified URL to any application resource. This is required and may never be an empty string.

#### HTTP_*
Variables matching the HTTP request headers sent by the client. The existence of these variables correspond with those sent in the current HTTP request.

#### leaf.url_scheme
Will be “http” or “https” depending on the HTTP request URL.

#### leaf.input
Will be a string representing the raw HTTP request body. If the HTTP request body is empty (e.g. with a GET request), this will be an empty string.

#### leaf.errors
Must always be a writable resource; by default, this is a write-only resource handle to `php://stderr`.

The Leaf application can store its own data in the environment, too. The environment array’s keys must contain at least one dot, and should be prefixed uniquely (e.g. “prefix.foo”). The prefix `leaf.` is reserved for use by Leaf itself and must not be used otherwise. The environment must not contain the keys `HTTP_CONTENT_TYPE` or `HTTP_CONTENT_LENGTH` (use the versions without HTTP_). The CGI keys (named without a period) must have String values. There are the following restrictions:

`leaf.url_scheme` must either be “http” or “https”.
`leaf.input` must be a string.
There must be a valid, writable resource in `leaf.errors`.
The `REQUEST_METHOD` must be a valid token.
The `SCRIPT_NAME`, if non-empty, must start with “/”
The `PATH_INFO`, if non-empty, must start with “/”
The `CONTENT_LENGTH`, if given, must consist of digits only.
One of `SCRIPT_NAME` or `PATH_INFO` must be set. `PATH_INFO` should be “/” if `SCRIPT_NAME` is empty. `SCRIPT_NAME` never should be “/”, but instead be an empty string.


<br>
<hr>

<a href="#/v/2.1-alpha/http/request" style="margin: 0px">Request</a>
<a href="#/v/2.1-alpha/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/v/2.1-alpha/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/2.1-alpha/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.1-alpha/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>