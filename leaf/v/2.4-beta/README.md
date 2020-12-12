# 📚 Getting Started

## Leaf PHP: v2.4 beta (New Roots)

New Roots is the latest beta release of Leaf PHP Framework. Unlike previous versions of Leaf, v2.4 looks to build up on existing features, and improves their usage by providing compatability upgrades as well as new methods which compliment use cases of those features. As such, all new features still center around existing implementations. Note that changes from this release will also be shipped in later versions of [LeafMVC](/), [LeafAPI](/) and [Skeleton](/).

<p class="alert -warning">
  v2.4 beta docs are still being updated, however, all breaking changes have already been documented. So feel free to upgrade to it and use it. You can open an issue for any bugs you find.
</p>

## 📁 Installation

Since this is a beta release, you'll have to specify that you want this version when installing Leaf.

```bash
composer require leafs/leaf ^2.4.0-beta
```

This command can also be run in your LeafMVC and LeafAPI projects to manually update leaf.

## 💡 What's New

Building a better experience for existing features doesn't necessarily mean that there's nothing new in Leaf. To view all the changes made to Leaf since the last release, you can check the [release notes](https://github.com/leafsphp/leaf/releases/tag/v2.4.0-beta). However, the major additions include:

- Auth settings
- Auth token lifetime
- Auth update
- Auth id and user
- Static Authentication and JWT methods
- Helper Db methods

There have also been huge fixes on the `Db` module and minor fixes generally throughout Leaf.

We also had to let go of a couple of features which had deprecation warnings in the previous version, and also some features which had exhausted their usefulness.

Read the [release notes](https://github.com/leafsphp/leaf/releases/tag/v2.4.0-beta) to view all changes.

**Note that the release notes are still being updated.**

<br>
<hr>

## Next steps

- [Intro](leaf/v/2.4-beta/intro/)
- [Configuring .htaccess](leaf/v/2.4-beta/intro/htaccess)
- [Your first leaf app](leaf/v/2.4-beta/intro/first)
- [Routing](leaf/v/2.4-beta/routing/)

<br>

Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
