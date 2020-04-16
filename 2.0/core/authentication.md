# Leaf Authentication
Authentication provides simple methods to help with manual authentication and working with tokens. If you want a much simpler way, you can check out [Simple Auth](2.0/core/auth).

## Working with tokens
Leaf provides you with the `JWT` object which includes various methods for creating and parsing token data....but we do not advice directly using the `JWT` object. For this reason, this object has been created to work with all the `JWT` data. You simply have to initialise it:

```js
$authentication = new Leaf\Authentication();
```

## Authentication methods:

### generateSimpleToken()
This method generates a new JSON Web Token. It takes 2 arguments. check out JWT for more info on JWT params

- (int) - A user id to encode
- (string) - A secret phrase to encode with the token

```js
$token = $authentication->generateSimpleToken(24', 'LEAF PHP SECRET CODE 1442');
```

### generateToken()
This method generates a new JSON Web Token: the same as `generateSimpleToken`, the only difference is that this method gives you more control over the token i.e. expiry time and custom fields. This method takes in 2 params, the entire `payload` of your JWT and a secret phrase. check out JWT for more info on JWT payload params.

- (array) - JWT payload
- (string) - A secret phrase to encode with the token

```js
$payload = [
	'iat' => time(),
	'iss' => 'localhost',
	'exp' => time() + (15*60),
	'userId' => $user_id,
	'username' => $username
];

$token = $authentication->generateToken($payload, "secret phrase");
```

### validateToken()
This method is used to confirm the identity of a token from an authorization header.

```js
$payload = $authentication->validateToken("SECRET PHRASE");
```

If the token is valid, it returns the decoded `payload`. So if we encode a payload:

```js
$payload = [
	'iat' => time(),
	'iss' => 'localhost',
	'exp' => time() + (15*60),
	'userId' => $user_id,
	'username' => $username
];
```

We can retrieve this payload by calling

```js
$payload = $authentication->validateToken("SECRET PHRASE");

$username = $payload["username"];
```

If the validation fails, it returns `false`, you can get any error by calling the `errors` method.

```js
$payload = $authentication->validateToken("SECRET PHRASE"); // returns false if failed

if ($payload == false) {
	$response->throwErr($authentication->errors());
}
```

### validate() <span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span>

This method is used to confirm the identity of a token. Unlike `validateToken`, the token to validate is directly passed into it. Just like `validateToken`, it returns the token's `payload`

```js
$payload = $authentication->validate($token, "SECRET PHRASE");

$username = $payload["username"];
```

If the validation fails, it returns `false`, you can get any error by calling the `errors` method.

```js
$payload = $authentication->validate($token, "SECRET PHRASE"); // returns false if failed

if ($payload == false) {
	$response->throwErr($authentication->errors());
}
```

### getBearerToken()
This method is used to get the bearer token from an authorization header. It returns `false` if there's no token. You can then use the `errors` method to retrieve any errors.

```js
$token = $authentication->getBearerToken();

// if there are any errors
if ($token == false) {
	echo $authentication->errors();
}
```

### getAuthorizationHeader()
This method is used to an authorization header. Returns `null` if anything goes wrong.

```js
$authHeader = $authentication->getAuthorizationHeader();
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