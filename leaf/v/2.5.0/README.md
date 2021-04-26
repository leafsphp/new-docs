# 📚 Getting Started

## Leaf PHP: v2.5.0 (💠 Gladiolus)

v2.5.0 continues to build up on existing features, and improves their usage by providing compatability upgrades as well as new methods which compliment use cases of those features.

However, unlike the v2.4 series, version 2.5 ships with new features, bug fixes and a whole lot of stripped code (no breaking changes besides removing default blade integration). Note that changes from this release will also be shipped in later versions of [LeafMVC](/leaf-mvc/), [LeafAPI](/leaf-api/) and [Skeleton](/skeleton/).

## 📁 Installation

You can install leaf quickly using composer.

```bash
composer require leafs/leaf
```

This command can also be run in your LeafMVC and LeafAPI projects to manually update leaf.

## 💡 What's New

Building a better experience for existing features doesn't necessarily mean that there's nothing new in Leaf. To view all the changes made to Leaf since the last release, you can check the [release notes](https://github.com/leafsphp/leaf/releases/tag/v2.5.0). However, the major changes include:

- Added Leaf flash for better flash message support
- Added etag based http caching
- Added support for flash messages on session
- Added new logging support for Leaf
- Current app instance is now available on `Leaf\Config`
- Session get returns null for unset variables instead of throwing an error
- Custom error pages now available right after initializing Leaf
- Fixed app logging
- Set helper is now a Container module
- Better middleware and hook support
- Removed unused middleware
- Removed unused code
- Removed leaf environment
- Removed default Leaf blade integration

**None of these changes besides blade break anything, they just provide better usability.**

<br>
<hr>

## Next steps

- [Intro](leaf/v/2.5.0/intro/)
- [Configuring .htaccess](leaf/v/2.5.0/intro/htaccess)
- [Your first leaf app](leaf/v/2.5.0/intro/first)
- [Routing](leaf/v/2.5.0/routing/)

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
