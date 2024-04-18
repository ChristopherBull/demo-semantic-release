# Demo: Automated Semantic releases and Conventional Commits

[Semantic Release](https://semantic-release.gitbook.io/semantic-release) is a tool used to automate the process of continuous delivery and deployment. It analyses the commit messages following the [Conventional Commit Messages](#conventional-commit-messages) format, generates release notes, and automatically increments the software version number according to the Semantic Versioning convention ([SemVer](http://semver.org/)). This allows for streamlined and consistent versioning and release management.

This demonstration repository will cover the following topics:

1. [Conventional Commits](#conventional-commit-messages): We will start by explaining what semantic commits are and how to write them. This will set the foundation for the rest of the process.

2. [Commitlint](#commitlint): Next, we will introduce Commitlint, a tool that helps enforce the structure of your commit messages.

3. [Git Hooks](#git-hooks): We will then delve into Git Hooks, which are scripts that Git executes before or after events such as `commit` and `push`. We will show how these can be used to automate the process of linting your commit messages (preventing non-conventional commits).

4. [Semantic Release](#semantic-release): Finally, we will explain how the Semantic Release tool works.

## Conventional Commit Messages

[Conventional commits](https://www.conventionalcommits.org/) are a style of writing commit messages. This convention provides a set of rules that specify what a commit message should contain and how to structure it. Standardising commit messages like this makes them easier for people to read, and convey correct and important information, and opens the door to automation opportunities within the development process. This allows, for example, other tools to auto-generate release notes and automatically increment the software version following [SemVer](http://semver.org/) (the Semantic Versioning convention).

A simple conventional commit will follow this structure:

```txt
<type>: <description>
```

A more detailed conventional commit message will look like this:

```txt
<type>[(optional scope)]: <description>

[optional body]

[optional footer(s)]
```

If you want to ensure that conventional commit messages are used (to prevent typos that break the schema or enforce collaborators to follow this convention), then you can consider tools for linting the commit messages and adding rules to a CI/CD or repo to halt a commit/push/pull_request if the commit message is not formatted correctly.

> [!TIP]
> If you have collaborators, consider adding or updating your repository's [guidelines for contributors](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/setting-guidelines-for-repository-contributors) which would specify what you expect from collaborators and include, for example, that commit messages use conventional commit format and are enforced with linting tools. This repository has a [brief CONTRIBUTING.md example](./CONTRIBUTING.md).

## Commitlint


## Git Hooks


## Semantic Release

