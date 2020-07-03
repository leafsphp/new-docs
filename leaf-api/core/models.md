# 📕 Leaf MVC Models

In Leaf API, we don't really have anything to do with our models: Leaf Core has taken all the trouble out of using models, so all we have to do in Leaf API is to generate the model and include it in our controller.

Our Models are kept in `App/Models`, but we won't need to create our models manually. Leaf MVC's command line tool covers this for us.

```bash
php leaf g:model <Name>
```

A new model will be created in the `App\Models` directory which looks like this:

```js
<?php
namespace App\Models;

class ClassName extends Model {

}
```

That's all we **need** to do with our model. Leaf API's models have methods prepared which allow us to manipulate out database without doing much.

We can create, read, update and delete without writing any code to specially access our database.

## Using a model

As mentioned earlier, we include models in our controller to use them. We can do that by using the `use` keyword.

```js
<?php
namespace App\Controllers;

// include the model
use App\Models\User;

class UserController extends Controller {
  public function index($id) {
    // use the model here
    $user = User::find($id);
    $this->respond($user);
  }
}
```

In our controller, we can do these:

```js
// return all rows
ModelName::all();

// return all rows sorted by date created
ModelName::orderBy('created_at', 'desc')->get()

// find a database row by id
ModelName::find($id);

// find a database row by title
ModelName::where('title', 'Title goes here')->get();

// create a new database row
$model = new ModelName;
$model->field = $this->request->get("field");
$model->save();

// delete a post
$model = ModelName::find($id);
$model->delete();
```

Read [Leaf Core Model docs](2.1/core/model) for more info on models.

Checkout [building your first app](/getting-started/first-app) for more practical use cases.

## Others

You can create a migration for your model by including the `-m` flag

```bash
php leaf g:model -m <ModelName>
```

### Model Help (Leaf Console)

```bash
Description:
  Create a new model class

Usage:
  g:model [options] [--] <model>

Arguments:
  model                 model file name

Options:
  -m, --migration       Create a migration for model
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
```

## Next Steps

- [Leaf Core Model](/2.1/core/model)
- [Leaf Core API Controllers](/2.1/core/api-controller)
- [Migrations](/leaf-api/core/migrations)
- [Views](/leaf-api/core/views)

Built with ❤ by [**Mychi Darko**](//mychi.netlify.app)
