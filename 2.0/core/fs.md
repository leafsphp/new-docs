# Leaf FS

This is a simple functionality inspired by node js' FileSystem(fs) module. Leaf FS aims to make directory and file management much simpler than what you're currently used to, so as to speed up and ease the dev process.😊👌😎

Leaf FS allows you to read/write to file, create, rename, copy and paste files/directories all with just a few lines of code. All this is performed while maintaining Leaf's simplicity.

**In v2, all FS methods have been rewritten in `snake_case`. Also, the `baseDirectory` concept has been discontinued**

## Including FS

To include the FS object in a route, use this:

```js
$fs = new Leaf\FS;
```

## FS Directory Methods

### create_folder

This will create a new directory in the `current directory`

Let's take this directory structure below, we initialise Leaf FS in our index.php file.

```bash
├───logs
├───index.php
```

In our index.php file:

```js
$fs->create_folder("new_logs");
```

After running this code, this is our new directory structure

```bash
├───logs
├───new_logs
├───index.php
```

<hr>

### rename_folder

rename_folder is used to rename a directory. It takes in two parameters: the directory you want to rename and it's new name/path.

```js
$fs->rename_folder("new");
$fs->rename_folder("home/new", "home/items");
```

<hr>

### delete_folder

delete_folder is used to delete a directory. It takes in two parameters: the directory you want to delete.

```js
$fs->delete_folder("new", "items");
$fs->delete_folder("home/new", "home/items");
```

<hr>

### list_dir

list_dir returns an array of all the files/folders in a directory. It takes in the directory to list and a search pattern eg: `*.php`. Also note that all folders end with a '/'

```js
$fs->list_dir("new");
$fs->list_dir("home/new", "*.txt");
```

<hr>

### FS File Methods

##### create_file

`create_file` is used to create a new file in the `current directory`. It takes in the filename or path+filename. If the file already exists, it gives the new file a different name.

```js
$fs->create_file("items.txt");
$fs->create_file("home/items.txt");
```

##### write_file

`write_file` is used to add content to a file, if the file already has content, all the content in there is replaced with the new content. Also, if the file doesn't exist, it will be created and all the content will be added to it. It takes in 2 parameters, the name/path+name of the file and the content;

```js
$fs->write_file("items.txt", "Hello");
$fs->write_file("items.txt", [
  	"name" => "Item 1"
]);
$fs->write_file("items.txt", 1);
```

##### append_file

append_file is almost exactly the same as write_file, except that instead of replacing the content in a file, it adds to the end of it.

```js
$data = $fs->append_file("items.txt", "Item name");
```

##### prepend_file <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 11px;">New in v2</span></sup>

prepend_file is almost exactly the same as write_file, except that instead of replacing the content in a file, it adds to the begining.

```js
$data = $fs->prepend_file("items.txt", "Item name");
```

##### read_file

read_file returns the data found in a file. It takes 1 parameter: the file name/path+file name.

```js
$data = $fs->read_file("./home/items.txt");
```

##### rename_file

rename_file renames a file. It takes 2 parameter: the file name/path+file name to rename and it's new name.

```js
$data = $fs->rename_file("./home/items.txt", "home/products.txt");
```

##### delete_file <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 11px;">New in v2</span></sup>

delete_file deletes a file. It takes 2 parameter: the file name/path+file name to delete.

```js
$data = $fs->delete_file("./home/items.txt");
```

##### copy_file

copy_file copies a file from the current directory to another directory. It takes in 3 parameters: the filename, the new path + filename and whether to rename the file if it exists in the new directory. The 3rd parameter is optional, if nothing is passed for the 3rd parameter, it will rename the file. Pass in true to rename the file if it already exists, false to override the file content(default is true).

```js
$data = $fs->copy_file("items.txt", "./home/");
$data = $fs->copy_file("items.txt", "./home/", false);
```

##### clone_file <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 11px;">New in v2</span></sup>

clone_file also copies a file from the current directory to another directory, but unlike copy_file, clone_file includes the filename, and it takes in 2 parameters: the filename and the path+filename to clone to.

```js
$data = $fs->clone_file("items.txt", "./home/products.txt");
```

##### move_file <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 11px;">New in v2</span></sup>

move_file also moves a file from the current directory to another directory, it takes in 2 parameters: the filename and the path to move to.

```js
$data = $fs->move_file("items.txt", "./home/");
```

##### upload <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 11px;">New in v2</span></sup>

upload is for simple file uploads. It takes in 3 parameters, the path to save the file, the file and the file type(optional). It returns an array `[true, $filename]` if successful and `[false, $error]` if the upload fails.

```js
$profilePic = $_FILES["profile_pic"];
// file upload
$fs->upload("./images/", $profilePic);
// file upload with file type
$fs->upload("./images/", $profilePic, "image");
```

##### chmod <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 11px;">New in v2</span></sup>

Get or set UNIX mode of a file or directory.

```js
$mode = $fs->chmod("items.txt");
$fs->chmod("items.txt", ...);
```

<!-- ##### link <sup><span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 11px;">New in v2</span></sup>
Create a symlink to the target file or directory. On Windows, a hard link is created if the target is a file.

```js
$mode = $fs->link("items.txt", "");
``` -->

<hr>

## FS Example

```js
$fs = new Leaf\FS;

$leaf->post('/books/add', function() use($fs) {
	$book = [
		"title" => "something.epub",
		"content" => "something"
	];
	$fs->create_folder("books");
	$fs->create_file("books/".$book["title"]);
	$fs->write_file("books/".$book["title"], $book["content"]);
	$fs->read_file("books/".$book["title"]);
});
```

This is a simple example where we create a folder, create a file in the new folder, add some data to that new file and read the data from the file.

<br>
<hr>

<a href="#/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>