# Leaf Tokens

Leaf token is a simple token "service" that uses a much simpler and cleaner syntax, also, it's very easy to work with, though not so secure at the moment. With that, it's only recommended for Personal Projects. Not to worry, Leaf Tokens will be receiving upgrades in later versions of Leaf.

## Including Leaf Token
To include the Token object in a route, use this:

```js
$token = new Leaf\Core\Token;
```

Leaf Token currently has security issues, therefore, it's not recommended for anything but personal projects
Unlike the tokens you're used to, Leaf token saves all data passed into it as an object which can be used later for authentication or something else.

## Token Methods

### generateSimpleToken
This method creates a simple base 64 token which contains JSON encoded data. It takes in 3 parameters, a username, a user id and an expiry time in seconds. The expiry time for the token is optional: if none is set, it sets the expiry time to 1 week.

```js
$token = new Leaf\Core\Token;

$userToken = $token->generateSimpleToken("Mychi Darko", 2, (7 * 24 * 60 * 60));
// $token->generateSimpleToken("username", "user id", "expiry time");
```

This will encode the data passed into it and return it as the token value.

### generateToken
As the name implies, generateToken also generates a base64 encoded token, the same as generateSimpleToken, but unlike generateSimpleToken, generateToken takes in 2 parameters: the token data to encode(don't forget to pass a `token_secret`) and the expiry time of the token. The expiry time for the token is optional: if none is set, it sets the expiry time to 1 week.

```js
$token = new Leaf\Core\Token;

$data = [
	"username" => "Mychi Darko",
	"email" => "mickdd22@gmail.com",
	"token_secret" => "tdt672d81d678"
];

$userToken = $token->generateToken($data, (7 * 24 * 60 * 60));

// $token->generateToken("data to encode", "expiry time");
```

This will encode the data passed into it and return it as the token value.

### validateToken
This is where Leaf Token gets interesting. Validate token just checks to see if the token is a valid leaf app token, also, it checks if the token is still active (not expired), from there, it just returns the token data. validateToken takes in just one parameter: the token returned from the user.

```js
$token = new Leaf\Token;

// Token data encoded
// $data = [
// 	"username" => "Mychi Darko",
// 	"email" => "mickdd22@gmail.com",
// 	"token_secret" => "tdt672d81d678"
// ];

$leaf->post('/login', function() use($token) {
	$data = $token->validateToken('token gotten from user......');
	$username = $data['username'];
});
```
With Leaf Token, you can save data in your token and retrieve it after validating the token, quite handy😎👌

<br>
<hr>

<a href="#/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>