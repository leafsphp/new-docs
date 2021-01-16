# Leaf Ecosystem

Leaf focuses on creating and maintaining PHP tools that help make creating websites, web apps and APIs quickly and as simply as possible. As such, all our tools focus on giving you the needed simplicity but at the same time give you a ton of functionality.

## Our Tools

### Leaf PHP (Core Package)

This is at the core of most of our libraries, but is also a full-fledged framework/library on it's own. Taking inspiration from slimphp and nodejs' simplicity, the power and flexibility of ruby on rails and laravel/lumen coupled with a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant web apps and APIs.

[Read the docs](/leaf/)

### Leaf MVC

Leaf MVC builds a simple to use structure around the [Leaf package](/leaf/) which allows you to use Leaf in an MVC setup. Not only is it easy to use and more structured, but very customizable as well. Coupled with features similar to bigger and more popular frameworks and a super smart console tool: [Aloe CLI](/aloe-cli/), Leaf MVC is the best way to build highly interactive and scalable web apps.

**Leaf MVC docs have migrated from leafmvc.netlify.app, acesss them here instead.**

[Read the docs](/leaf-mvc/)

### Leaf API

Leaf API builds on the setup provided by Leaf MVC but takes it in a direction geared for API development. Let's just say you get to enjoy Leaf MVC but with features for API development. Leaf API is intuitive, scalable, easy to use and customize and more importantly works the way you want it to.

[Read the docs](/leaf-api/)

### Skeleton

Skeleton takes quite a different turn from the packages above in a sense that instead of a framework/library, skeleton is more of a boilerplate. Skeleton takes the cool features of the above packages, packs in aloe cli and removes all the restrictions that come along with those systems.

[View on github](/skeleton/)

### Aloe CLI

Aloe CLI is the sole console tool that powers Leaf MVC, Leaf API and Skeleton. Aloe is probably the smartest PHP console tool in existence today. Aloe packs in a ton of functionality and customizations unto the symfony CLI. Aloe doesn't only provide great commands with easy integrations, but also gives you a cleaner and more elegant syntax to write your commands.

[Read the docs](/aloe-cli/)

These are the main packages being actively developed, however there are still more packages which we've developed over time. These are either used internally by some of the above packages or have their development moving very slowly.

### Leaf Blade

Leaf blade is the adaptation of [jessenger's blade package](.) used within Leaf apps. Leaf blade adds some extra methods to the original package which allows Leaf to easily hook into blade.

[View on github](/aloe-cli/)

### Leaf UI

If you've used flutter or react, chances are that you prefer using objects to build UIs instead of strings. PHP allows you to output HTML as strings to build your UI, this method is pretty redundant and can cause issues especially with quotes. Inspired by XHP, flutter and JSX, Leaf UI allows you to build UIs using PHP objects instead of strings.

[Read the docs](/ui/)
