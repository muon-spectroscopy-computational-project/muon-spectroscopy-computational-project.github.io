Thank you for your interest in contributing to std-re[p! We welcome contributions from the community to make our project better.

## Table of Contents

1. [How to Contribute](#how-to-contribute)
    - [Reporting Bugs](#reporting-bugs)
    - [Requesting Features](#requesting-features)
    - [Creating Pull Requests](#creating-pull-requests)
2. [Coding Standards](#coding-standards)
    - [Code Style](#code-style)
    - [Commit Messages](#commit-messages)
3. [Testing](#testing)
4. [Documentation](#documentation)




## How to Contribute

### Reporting Bugs

If you find a bug or unexpected behaviour, please help us by creating an issue by following the steps below.
1. Go to the repository that you like to report the bug.
2. Click on the issues tab.
3. Click on the `New Issue` button.
4. From the list of options select `Bug report`.
5. Provide a clear and detailed description of the issue, including steps to reproduce it.

### Requesting Features

We're open to feature suggestions! If you have an idea for a new feature or improvement, please create a feature request by following the steps below.
1. Go to the repository that you like to report the bug.
2. Click on the issues tab.
3. Click on the New Issue button.
4. From the list of options select `Feature request`.
5. Provide a clear and detailed description of the feature.

### Creating Pull Requests

Before submitting a pull request, please ensure that:

- Your changes have been tested.
- Your code follows our coding standards.
- Your commits have clear and concise messages.

If you're ready to submit a pull request:

1. Fork the repository and create a new branch.
2. Make your changes and test them thoroughly.
3. Commit your changes with descriptive commit messages.
4. Push your branch to your fork.
5. Open a pull request with a clear title and description.

## Coding Standards

### Code Style

For the python project follow the [PEP8](https://peps.python.org/pep-0008/) Coding standards. <br>
For the c++ projects follow the [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html), if not mentioned otherisie in the README.MD of the repository.

### Commit messages
- The commit message is mainly for the other people, so they should be able to understand it now and six months later. 
- Always add a brief description of the commit to the first line of the commit and terminate by two newlines (it will work without the second newline, but that is not nice for the interfaces). 
- Each line in description must not exceed 75 characters (there is no limit on number of lines). 
- When committing code on behalf of others use the --author option, e.g. git commit -a --author "Joe Coder <joe@coder.org>". 
- Use the imperative form of verbs rather than past tense when referring to changes introduced by commit in question. For example "Remove property X" rather than "Removed property X".

#### Example
```
Short explanation of the commit

Longer explanation explaining exactly what's changed and why, whether
any external or private interfaces changed, what issue were fixed (with
issue number if applicable) and so forth. Be concise but not too brief.

```

<sup> ref: [wiki.gnome.org](https://wiki.gnome.org/Git/ CommitMessages)</sup>

## Testing
Writing test is essential for the reliability and maintainability of the code. Place your tests in the tests directory at the root of the project.

- A testing unit should focus  on one tiny bit of functionality and prove it correct.
- Each test unit must be fully independent
- Try the best to make the test run fast

## Documentation

- Before submitting your contribution, preview your documentation changes locally following the instructions in the respective repositories.
- Maintain a consistent writing style across the documentation. Follow the project's established conventions.
- If your documentation includes images or other media, ensure they are placed in the correct directory and referenced appropriately.
- If referencing other sections or documents, use relative links to maintain consistency.
- If your changes impact the structure of the documentation, make sure to update the Table of Contents.

