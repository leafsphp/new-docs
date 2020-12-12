# 📚 Getting Started

## Leaf PHP v2.2 BETA

Leaf v2.2 beta is the latest beta release of Leaf PHP Framework that comes along with a bunch of new features, better functionality and fixes from v2.1.

## 📁 Installation

You can view installation for Leaf v2.2 beta [here](leaf/v/2.2-beta/intro/)

## What's New

### 📑 Added <sup class="new-tag-1">New in v2.2 beta</sup>

- Added `Leaf\Auth::currentUser`
- Added new cookies package relying on PHP's `setcookie`

### 🔧 Fixed

- fixed hidden fields on `Leaf\Auth::login`
- Fixed multiple-request type data on `get` and `body` at `Leaf\Http\Request`

### 🎈 Changed

- Switched cookies package in `Leaf\Http\Response`
- Switched cookies package in `Leaf\App`

### 🚚 Removed

- Removed old cookies package and all it's methods
- Removed `setEncryptedCookie` and `getEncryptedCookie` on `Leaf\App`
- Slashed unnecessary code from `Leaf\Http\Request`

<br>
<hr>

<a href="#/leaf/v/2.2-beta/intro/htaccess" style="margin: 0px;">Re-routing to index</a>
<a href="#/leaf/v/2.2-beta/intro/first" style="margin: 0px 10px;">Building your first leaf app</a>
<a href="#/leaf/v/2.2-beta/routing/" style="margin: 0px 10px;">Routing</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
