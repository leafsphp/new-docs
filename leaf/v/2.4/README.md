# 📚 Getting Started

## Leaf PHP: v2.4.1 (🍁 Marvel-of-peru)

🍁 Marvel-of-peru is the latest stable release of Leaf PHP Framework. Just like the previous beta, v2.4 looks to build up on existing features, and improves their usage by providing compatability upgrades as well as new methods which compliment use cases of those features. As such, all new features still center around existing implementations. Note that changes from this release will also be shipped in later versions of [LeafMVC](/), [LeafAPI](/) and [Skeleton](/).

<p class="alert -warning">
  v2.4.0 has been revised into v2.4.1 due to some internal issues with stand-alone use.
</p>

## 📁 Installation

You can install leaf quickly using composer.

```bash
composer require leafs/leaf
```

This command can also be run in your LeafMVC and LeafAPI projects to manually update leaf.

## 💡 What's New

Building a better experience for existing features doesn't necessarily mean that there's nothing new in Leaf. To view all the changes made to Leaf since the last release, you can check the [release notes](https://github.com/leafsphp/leaf/releases/tag/v2.4.1). However, the major additions include:

- New auth settings
- Added `Route::view`
- New Factory class for MVC, API and Skeleton
- Added support for session based authentication instead of just JWT
- Fixed all known bugs from previous versions
- Separated Router module from app module
- Removed app down feature from v2.4.0

There have also been huge fixes on the `Db` and `Auth` modules and minor fixes generally throughout Leaf.

We also had to let go of a couple of features which had deprecation warnings in the previous version, and also some features which had exhausted their usefulness.

Read the [release notes](https://github.com/leafsphp/leaf/releases/tag/v2.4.1) to view all changes.

**Note that the release notes are still being updated.**

<br>
<hr>

## Next steps

- [Intro](leaf/v/2.4/intro/)
- [Configuring .htaccess](leaf/v/2.4/intro/htaccess)
- [Your first leaf app](leaf/v/2.4/intro/first)
- [Routing](leaf/v/2.4/routing/)

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
