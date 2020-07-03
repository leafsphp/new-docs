# 📕 Leaf API Envionment Config

Leaf API tries to maintain a working-out-of-the-box configuration as much as possible, so, for the most part, you don't have to configure anything.

Any configuration done in Leaf API is not done for Leaf API, but rather for your application. All config for your app is found in the `.env` file, found in your project root.

## .env

By default, it should look like this:

```env
APP_NAME=LEAF_API
APP_ENV=local
APP_KEY=base64:AUAyDriQD1kFdIbwTHlnCm2pYn+qxDBa55SFwB9PUzg=
APP_DEBUG=true
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=LEAF_DB_NAME
DB_USERNAME=LEAF_DB_USERNAME
DB_PASSWORD=

MAIL_DRIVER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null

PROD_SERVER=hello
PROD_PORT=22
PROD_USER=leaf
APPLICATION_DIR=leaf
APPLICATION_PATH=leaf
```

As you can see the settings are divided into 4 parts:

### App Config

This part entails general app information.

### Db Config

This section holds all your database connection variables:

- DB_CONNECTION - DB type
- DB_HOST - DB Hostname
- DB_PORT - DB connection port
- DB_DATABASE - Database to connect to
- DB_USERNAME - Username for database
- DB_PASSWORD - Password for db

These are the settings you would mostly be using in your apps

### Mail Config

These settings are related to emailing.

- MAIL_DRIVER - Connection driver
- MAIL_HOST - The email host to connect to
- MAIL_PORT - Port to use
- MAIL_USERNAME - Username
- MAIL_PASSWORD - Password
- MAIL_ENCRYPTION - Email Encryption

### Deployment Config

This section hold deployment config

## Using Environment Variables

Variables defined in the `.env` file can be used in your app by calling the `env` or `getenv` methods.

```js
$app_name = env("APP_NAME");
$db_name = getenv("DB_DATABASE");
```

## Next Steps

- [Models](/leaf-api/core/models)
- [Controllers](/leaf-api/core/controllers)
- [Views](/leaf-api/core/views)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
