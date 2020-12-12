# 📕 Leaf API Migrations

For those who struggle with maintaining their database schema, or who have problems applying updates and often revert them, there is a solution. Leaf API migrations basically help in creating and manipulating database.

## Generating a migration

You can quickly generate a migration using the `g:migration` [Leaf Console](/leaf-api/v/1.1/utils/console) command:

```bash
php leaf g:migration <Name>
```

The new migration will be placed in your `App/Database/Migrations` directory. Each migration file name begins with a timestamp.

## Migration Structure

A migration class contains two methods: up and down. The up method is used to add new tables, columns, or indexes to your database, while the down method should reverse the operations performed by the up method.

You can create and modify tables in the both of these methods. In this example, we create a posts table:

```php
<?php
namespace App\Database\Migrations;

use Leaf\Database;

class CreateUsers extends Database {
  public function __construct() {
    parent::__construct();
  }

  /**
   * Run the migrations.
   *
   * @return void
   */
  public function up()  {
    if(!$this->capsule::schema()->hasTable("posts")):
      $this->capsule::schema()->create("posts", function ($table) {
        $table->increments('id');
        $table->string('author_id');
        $table->string('title');
        $table->text('body');
        $table->timestamps();
      });
    endif;
  }

  /**
    * Reverse the migrations.
    *
    * @return void
    */
  public function down() {
    $this->capsule::schema()->dropIfExists("posts");
  }
}
```

## Running a migration

To run all of your outstanding migrations, execute the `db:migrate` command:

```bash
php leaf db:migrate
```

## Rolling Back Migrations

To roll back the latest migration operation, you may use the `db:rollback` command.

```bash
php leaf db:rollback <step>
```

The `step` option allows you roll back a limited number of migrations. For example, the following command will roll back the last two migrations:

```bash
php leaf db:rollback 2
```

To roll back all migrations, you can just pass `all` as the `step` option.

```bash
php leaf db:rollback all
```

## Next Steps

The idea for Leaf API migrations was based on Laravel migrations, so you can read [Laravel migrations](https://laravel.com/docs/7.x/migrations) for a better understanding.

- [Views](/leaf-api/v/1.1/core/views)
- [Leaf Core Model](/leaf/v/2.1/core/model)
- [Leaf Core API Controllers](/leaf/v/2.1/core/api-controller)
- [Leaf Auth](/leaf/v/2.1/core/auth)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
