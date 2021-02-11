<!-- markdownlint-disable no-inline-html -->
# 📂 Leaf FS

This is a simple functionality inspired by node js' FileSystem(fs) module. Leaf FS aims to make directory and file management much simpler than what you're currently used to, so as to speed up and ease the dev process.😊👌😎

Leaf FS allows you to read/write to file, create, rename, copy and paste files/directories all with just a few lines of code. All this is performed while maintaining Leaf's simplicity.

<div class="alert -info">
In v2.4, all FS methods have been made static, and can now be called from anywhere in your application.
</div>

## Including FS

To include the FS object in a route, use this:

```php
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

```php
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

```php
$fs->rename_folder("new");
$fs->rename_folder("home/new", "home/items");
```

<hr>

### delete_folder

delete_folder is used to delete a directory. It takes in two parameters: the directory you want to delete.

```php
$fs->delete_folder("new", "items");
$fs->delete_folder("home/new", "home/items");
```

<hr>

### list_dir

list_dir returns an array of all the files/folders in a directory. It takes in the directory to list and a search pattern eg: `*.php`. Also note that all folders end with a '/'

```php
$fs->list_dir("new");
$fs->list_dir("home/new", "*.txt");
```

<hr>

### FS File Methods

#### create_file

`create_file` is used to create a new file in the `current directory`. It takes in the filename or path+filename. If the file already exists, it gives the new file a different name.

```php
$fs->create_file("items.txt");
$fs->create_file("home/items.txt");
```

#### write_file

`write_file` is used to add content to a file, if the file already has content, all the content in there is replaced with the new content. Also, if the file doesn't exist, it will be created and all the content will be added to it. It takes in 2 parameters, the name/path+name of the file and the content;

```php
$fs->write_file("items.txt", "Hello");
$fs->write_file("items.txt", [
  "name" => "Item 1"
]);
$fs->write_file("items.txt", 1);
```

#### append_file

append_file is almost exactly the same as write_file, except that instead of replacing the content in a file, it adds to the end of it.

```php
$data = $fs->append_file("items.txt", "Item name");
```

#### prepend_file

prepend_file is almost exactly the same as write_file, except that instead of replacing the content in a file, it adds to the begining.

```php
$data = $fs->prepend_file("items.txt", "Item name");
```

#### read_file

read_file returns the data found in a file. It takes 1 parameter: the file name/path+file name.

```php
$data = $fs->read_file("./home/items.txt");
```

#### rename_file

rename_file renames a file. It takes 2 parameter: the file name/path+file name to rename and it's new name.

```php
$data = $fs->rename_file("./home/items.txt", "home/products.txt");
```

#### delete_file

delete_file deletes a file. It takes 2 parameter: the file name/path+file name to delete.

```php
$data = $fs->delete_file("./home/items.txt");
```

#### copy_file

copy_file copies a file from the current directory to another directory. It takes in 3 parameters: the filename, the new path + filename and whether to rename the file if it exists in the new directory. The 3rd parameter is optional, if nothing is passed for the 3rd parameter, it will rename the file. Pass in true to rename the file if it already exists, false to override the file content(default is true).

```php
$data = $fs->copy_file("items.txt", "./home/");
$data = $fs->copy_file("items.txt", "./home/", false);
```

#### clone_file

clone_file also copies a file from the current directory to another directory, but unlike copy_file, clone_file includes the filename, and it takes in 2 parameters: the filename and the path+filename to clone to.

```php
$data = $fs->clone_file("items.txt", "./home/products.txt");
```

#### move_file

move_file also moves a file from the current directory to another directory, it takes in 2 parameters: the filename and the path to move to.

```php
$data = $fs->move_file("items.txt", "./home/");
```

#### upload_file <sup class="new-tag-1">New in v2.4</sup>

<div class="alert -warning">
This method was previously upload. In v2.4, upload_file has received a lot of fixes and new features. Also the older upload method has been removed.
</div>

`upload_file` as the name suggests is a method that makes file uploading a breeze. This is the main highlight of `Leaf\FS` in v2.4. Also unlike in earlier versions, `upload_file` supports more type of files.

It takes in 3 parameters:

- The file to upload
- The path to save the file
- Config for file upload

```php
$profilePic = $request->files("profile_pic");

// file upload
Leaf\FS::upload_file($profilePic, "./images/");
```

One amazing thing about FS is that it can detect the type of file you're trying to upload and handle it accordingly, so you don't need to worry about that. Below is a table of common file types which are automatically detected.

| File Type         | Common Extensions                                    |
| :--------------  | :----------------------------------------------  |
|  image            | 'jpg', 'jpeg', 'png', 'gif', 'webp', 'apng', 'tif', 'tiff', 'svg', 'pjpeg', 'pjp', 'jfif', 'cur', 'ico' |
|  video             | 'mp4', 'webm', 'swf', 'flv'                              |
|  audio             |'wav', 'mp3', 'ogg', 'm4a'                              |
|  text                |'txt', 'log', 'xml', 'doc', 'docx', 'odt', 'wpd', 'rtf', 'tex', 'pdf' |
|  presentation |'ppsx', 'pptx', 'ppt', 'pps', 'ppsm', 'key', 'odp' |
|  compressed  |'zip', 'rar', 'bz', 'gz', 'iso', 'tar.gz', 'tgz', 'zipx', '7z', 'dmg'|
|  spreadsheet  |'ods', 'xls', 'xlsx', 'xlsm'                                  |
|  application    |'apk', 'bat', 'cgi', 'pl', 'com', 'exe', 'gadget', 'jar', 'msi', 'py', 'wsf' |

You can open an issue if you think there should be a new category or if an important extension is not present here.

**Upload Config**:

You can configure file uploads to behave the way you want it to, and that's the 3rd parameter it takes in.

```php
Leaf\FS::upload_file($profilePic, "./images/", []);
```

Config is an array that takes in particular properties:

```php
Leaf\FS::upload_file($profilePic, "./images/", [
  "verify_dir" => true
]);
```

This is a list of config options.

| Config Name  | Description                                                   | Possible Values           |
| :--------------  | :----------------------------------------------  |  -----------------------: |
|  unique           | If `true`, a timestamp is added to filename | `true`, `false`               |
|  verify_dir       | Add error if upload directory is invalid        | `true`, `false`               |
|  verify_file      | Add error if same filename exists                 | `true`, `false`               |
|  max_file_size | Set maximum file size in bytes, default: 10mb | integer                   |
|  file_type        | Set file type if it's not included in default list | string                       |
|  validate         | Validate file type for invalid extensions: Only works with the default extensions | `true`, `false`               |

If the file upload is successful, it returns the filename, you can perform whatever operation you need on the filename, if it fails you can access the errors through the `errors` method. Refer to error handling for this part.

```php
$filename = $fs->upload_file($profilePic, "./images/", []);
```

#### upload_info <sup class="new-tag-1">New in v2.4</sup>

When the file successfully uploads, records on the file details are shelved. You can access these with the `upload_info` method. It takes in one optional parameter, the name of the file whose info you want to return.

```php
// returns info on all uploaded files (associative array)
$uploadInfo = Leaf\FS::upload_info();

// returns info on only selected file
$profileInfo = $fs->upload_info($filename);
```

#### chmod

Get or set UNIX mode of a file or directory.

```php
$mode = $fs->chmod("items.txt");
$fs->chmod("items.txt", ...);
```

<!-- #### link
Create a symlink to the target file or directory. On Windows, a hard link is created if the target is a file.

```php
$mode = $fs->link("items.txt", "");
``` -->

<hr>

## FS Example

```php
$fs = new Leaf\FS;

$app->post('/books/add', function() use($fs) {
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

<a href="#/v/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/v/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/v/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
