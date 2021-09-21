# Leaf PHP Contributing Guide

Hi! I'm really excited that you are interested in contributing to Leaf. Before submitting your contribution, please make sure to take a moment and read through the following guidelines:

- [Code of Conduct](#code-of-conduct)
- [Pull Request Guidelines](#pull-request-guidelines)
- [Development Setup](#development-setup)
- [Project Structure](#project-structure)

## Code of Conduct

As contributors and maintainers of this project, we pledge to respect all people who contribute through reporting issues, posting feature requests, updating documentation, submitting pull requests or patches, and other activities.

We are committed to making participation in this project a harassment-free experience for everyone, regardless of the level of experience, gender, gender identity and expression, sexual orientation, disability, personal appearance, body size, race, age, or religion.

Examples of unacceptable behavior by participants include the use of sexual language or imagery, derogatory comments or personal attacks, trolling, public or private harassment, insults, or other unprofessional conduct.

Project maintainers have the right and responsibility to remove, edit, or reject comments, commits, code, wiki edits, issues, and other contributions that are not aligned to this Code of Conduct. Project maintainers who do not follow the Code of Conduct may be removed from the project team.

Instances of abusive, harassing, or otherwise unacceptable behavior may be reported by opening an issue or contacting one or more of the project maintainers.

This Code of Conduct is adapted from the [Contributor Covenant](http://contributor-covenant.org), version 1.0.0, available at [http://contributor-covenant.org/version/1/0/0/](http://contributor-covenant.org/version/1/0/0/)

## Pull Request Guidelines

- The `master` branch is just a snapshot of the latest stable release. All development should be done in dedicated branches. **Do not submit PRs against the `master` branch.**

- Checkout a topic branch from the relevant branch, e.g. `dev`, and merge back against that branch.

- It's OK to have multiple small commits as you work on the PR - GitHub will automatically squash it before merging.

- If adding a new feature:
  - Add accompanying test case.
  - Provide a convincing reason to add this feature. Ideally, you should open a suggestion issue first and have it approved before working on it.

- If fixing bug:
  - If you are resolving a special issue, add `(fix #xxxx[,#xxxx])` (#xxxx is the issue id) in your PR title for a better release log, e.g. `update entities encoding/decoding (fix #3899)`.
  - Provide a detailed description of the bug in the PR.

## Development Setup

You will need PHP 7.2 + and [composer](https://getcomposer.org).

After cloning the repo, run:

```bash
composer install
```

## Project Structure

- **`src`**: contains the source code.

  - **`Exception/`**: contains code for the general leaf exceptions.

    This contains default error states and screens for errors, down-times and the like. It also contains extensible mark-up and logging to keep track of errors. Basically, anything relating to errors.

  - **`Helpers/`**: contains default leaf utilities like the container (DI container).

  - **`App.php`**: contains initializers and main leaf code.
  
  - **`Config.php`**: class for configuring how leaf behaves.
  
  - **`Middleware.php`**: base class for creating leaf middleware.
  
  - **`Router.php`**: leaf router.
  
  - **`View.php`**: view config for leaf.

## Financial Contribution

As a pure community-driven project without any corporate backing, we also welcome financial contributions via OpenCollective.

- [Become a backer or sponsor on OpenCollective](https://opencollective.com/leaf)

## Credits

Thank you to all the people who have already contributed to Leaf!

<a href="https://github.com/vuejs/vue/graphs/contributors">
    <img src="https://opencollective.com/leaf/contributors.svg?width=890" />
</a>
