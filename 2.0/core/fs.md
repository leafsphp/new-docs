# Leaf FS

This is a simple functionality inspired by node js' FileSystem(fs) module. Leaf FS aims to make directory and file management much simpler than what you're currently used to, so as to speed up and ease the dev process.😊👌😎

Leaf FS allows you to read/write to file, create, rename, copy and paste files/directories all with just a few lines of code. All this is performed while maintaining Leaf's simplicity.

## Including FS
To include the FS object in a route, use this:

```js
$fs = new Leaf\FS(__DIR__);
```

When initialising leaf FS, don't forget to pass in the base directory, you can use `__DIR__` or `"./"` to set the base directory to the directory the file you're initialising Leaf FS is in.

```js
$fs = new Leaf\FS("./");
```

## FS Directory Methods
### Setting the Base Directory
Setting the base directory will change the folder you're working in...FS methods to read files and more will search the new base directory.

```js
$fs->setBaseDirectory("./path/to/new/base/dir");
```

<hr>

### Returning the Base Directory
In case you need to find the current base directory.

```js
$fs->getBaseDirectory();
```

<hr>

### mkDir
This will create a new directory in the `current directory`, not in the `base directory`

Let's take this directory structure below, we initialise Leaf FS in our index.php file.
```
├───logs
├───index.php
```

In our index.php file:
```js
// set the base directory to logs
$fs->setBaseDirectory("logs");
// create folder
$fs->mkDir("new_logs");
```

After running this code, this is our new directory structure

```
├───logs
├───new_logs
├───index.php
```

mkDir uses the current dir that `index.php` file is in

You can also pass a path to mkDir

```js
$fs->makeDir("./home/items");
```

<hr>

### mkDirInBase

`mkDirInBase` is exactly the same as `mkDir`, except that `mkDirInBase` creates a new folder in the `base directory`.

```js
$fs->mkDirInBase("new");
```

<hr>

### renameDir

renameDir is used to rename a directory. It takes in two parameters: the directory you want to rename and it's new name/path.

```js
$fs->renameDir("new", "items");
$fs->renameDir("home/new", "home/items");
```

<hr>

### FS File Methods
##### createFile

`createFile` is used to create a new file in the `base directory`. It takes in the filename or path+filename. If the file already exists, it gives the new file a different name.

```js
$fs->createFile("items.txt");
$fs->createFile("home/items.txt");
```

##### upload <span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span>
upload is for simple file uploads. It takes in 3 parameters, the path to save the file, the file and the file type(optional). It returns an array `[true, $filename]` if successful and `[false, $error]` if the upload fails.

```js
$profilePic = $_FILES["profile_pic"];
// file upload
$fs->upload("./images/", $profilePic);
// file upload with file type
$fs->upload("./images/", $profilePic, "image");
```

##### writeFile
`writeFile` is used to add content to a file, if the file already has content, all the content in there is replaced with the new content. Also, if the file doesn't exist, it will be created and all the content will be added to it. It takes in 2 parameters, the name/path+name of the file and the content;

```js
$fs->writeFile("items.txt", "Hello");
$fs->writeFile("items.txt", [
  	"name" => "Item 1"
]);
$fs->writeFile("items.txt", 1);
```

##### appendFile
appendFile is almost exactly the same as writeFile, except that instead of replacing the contant in a file, it adds to it.

```js
$data = $fs->appendFile("items.txt", "Item name");
```

##### readFile
readFile returns the data found in a file. It takes 1 parameter: the file name/path+file name.

```js
$data = $fs->readFile("./home/items.txt");
```

##### renameFile
renameFile renames a file. It takes 2 parameter: the file name/path+file name to rename and it's new name.

```js
$data = $fs->renameFile("./home/items.txt", "home/products.txt");
```

##### copyFile
copyFile copies a file from the base directory to another directory. It takes in 3 parameters: the filename, the new path + filename and whether to rename the file if it exists in the new directory. The 3rd parameter is optional, if nothing is passed for the 3rd parameter, it will rename the file. Pass in true to rename the file if it already exists, false to override the file content.

```js
$data = $fs->copyFile("items.txt", "./home/");
$data = $fs->copyFile("items.txt", "./home/", false);
```

##### copyToFile
copyToFile also copies a file from the base directory to another directory, but unlike copyFile, copyToFile includes the filename, and it takes in 2 parameters: the filename and the path+filename to rename to.

```js
$data = $fs->copyFile("items.txt", "./home/products.txt");
```

<hr>

## FS Example
```js
$fs = new Leaf\FS(__DIR__);

$leaf->post('/books/add', function() use($fs) {
	$book = [
		"title" => "something.epub",
		"content" => "something"
	];
	$fs->mkDir("books");
	$fs->setBaseDirectory("books");
	$fs->createFile($book["title"]);
	$fs->writeFile($book["title"], $book["content"]);
	$fs->readFile($book["title"]);
});
```

This is a simple example where we create a folder, set our working directory to the new folder, then we create a file in the new folder and add some data to that new file.
Before we move on, keep in mind that the base directory in Leaf FS refers to the current working directory, changing the base directory is just like using cd in a terminal.

<br>
<hr>

<a href="#/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>