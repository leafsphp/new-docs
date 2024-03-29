# Aloe Cli

<p class="alert -warning">
  Aloe CLI v1.2.11 (Art Aloe) has just been released.
  <a href="https://leafphp.dev/aloe-cli/">Read the docs</a>
</p>

Aloe is a simple but powerful console service that makes building your leaf apps just a simple walk in the park. Aloe CLI ships with the default Leaf console tool in the newer versions of Leaf API, soon in Leaf MVC and Leaf API.

Aloe comes with a predefined set of commands which provide project scaffolding, database and app management right from the console. It also introduces a much simpler and cleaner way to write your commands.

## Aloe List

```bash
Leaf MVC v2.0

Usage:
  command [options] [arguments]

Options:
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Available commands:
  example        example command's description
  help           Displays help for a command
  interact       Interact with your application
  list           Lists commands
  serve          Start the leaf development server
 aloe
  aloe:config    Install aloe config
 app
  app:down       Place app in maintainance mode
  app:up         Remove app from maintainance mode
 d
  d:command      Delete a console command
  d:controller   Delete a controller
  d:factory      Delete a model factory
  d:migration    Delete a migration
  d:model        Delete a model
  d:seed         Delete a model seeder
 db
  db:install     Create new database from .env variables
  db:migrate     Run the database migrations
  db:rollback    Rollback all database migrations
  db:seed        Seed the database with records
 env
  env:generate   Generate .env file
 g
  g:command      Create a new console command
  g:controller   Create a new controller class
  g:factory      Create a new model factory
  g:helper       Create a new helper class
  g:migration    Create a new migration file
  g:model        Create a new model class
  g:seed         Create a new seed file
  g:template     Create a new view file
 scaffold
  scaffold:auth  Scaffold basic app authentication
```

## Next Steps

- [Misc Aloe Commands](/aloe-cli/v/1.1.0/commands/misc-commands)
- [Custom commands](/aloe-cli/v/1.1.0/commands/custom)
- [Commands IO](/aloe-cli/v/1.1.0/commands/io)
- [Creating Libraries](/aloe-cli/v/1.1.0/libraries)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
