# 📚 Getting Started

## Leaf PHP: Lucky Charm🍀

Lucky Charm🍀 is the latest stable release of Leaf PHP Framework. It comes with fixes for most known bugs, sharper and simpler looking methods, a smaller package size, better data handling and suggestions from our community. Note that changes from lucky charm will also be shiped in later versions of [LeafMVC](/), [LeafAPI](/) and [Skeleton](/).

## 📁 Installation

You can view installation for Lucky Charm🍀 [here](leaf/v/lucky-charm/intro/)

## What's New

### 📑 Added <sup class="new-tag-1">New in Lucky Charm🍀</sup>

- Added `Leaf\Auth::useToken`
- Added `Leaf\FS::upload_file`
- Added manual init to `Leaf\Session`
- Added option for status code messages
- Added callable utils
- Added session encoding/decoding
- `Leaf\Http\Request` now catches files passed into request
- Added `Leaf\Http\Request::typeIs`
- `Leaf\Http\Request::get` can now return multiple request data at once
- Added `Leaf\Http\Request::files`

### 🔧 Fixed

- fixed `Leaf\Http\Headers`
- Fixed response http status codes bug
- Fixed header integration with response
- Fixed header reliance on `Set`
- Fixed `throwErr` code error
- Fixed `Leaf\Session` package
- Fixed response redirect
- Fixed `Leaf\Http\Request::body` bugs  
- Sessions return `false` instead of throwing errors (Fix for web apps)
- FS returns `false` instead of throwing errors
- Fixed up `Leaf\Http\Request::params`
- Fixed up `Leaf\Http\Request::hasHeader`
- Fixed up header related methods on `Leaf\Http\Request`
- Fixed bugs on `Leaf\Environment`

### 🎈 Changed

- Switched `Leaf\Session` to native PHP sessions
- Switched session package in `Leaf\App`
- Changed controller file uploads to `Leaf\FS`
- `Leaf\Date` methods can now be called static-ly
- Switched `Leaf\Date` methods to camel case, but with backward compatability for snake_case
- Made all `Leaf\FS` methods static

### 🚚 Removed

- Removed old session code
- Removed `setEncryptedCookie` and `getEncryptedCookie` on `Leaf\App`
- Slashed unnecessary code from `Leaf\Http\Request`
- Slashed unnecessary code from `Leaf\Http\Session`
- Slashed unnecessary code from `Leaf\Http\Cookie`
- Slashed unnecessary code from `Leaf\Http\Response`
- Removed all method type tests from `Leaf\Http\Request`

<br>
<hr>

<a href="#/leaf/v/lucky-charm/intro/htaccess" style="margin: 0px;">Re-routing to index</a>
<a href="#/leaf/v/lucky-charm/intro/first" style="margin: 0px 10px;">Building your first leaf app</a>
<a href="#/leaf/v/lucky-charm/routing/" style="margin: 0px 10px;">Routing</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
