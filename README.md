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

If you want to ensure that conventional commit messages are used (to prevent typos that break the schema or enforce collaborators to follow this convention), then you can consider tools for linting the commit messages and adding rules to a CI/CD or repo to halt a commit/push/pull_request if the commit message is not formatted correctly. Tools for release management, such as [Commitizen](https://commitizen-tools.github.io/commitizen/), can also provide step-by-step prompts to remind you how to construct conventional commits.

> [!TIP]
> If you have collaborators, consider adding or updating your repository's [guidelines for contributors](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/setting-guidelines-for-repository-contributors) which would specify what you expect from collaborators and include, for example, that commit messages use conventional commit format and are enforced with linting tools. This repository has a [brief CONTRIBUTING.md example](./CONTRIBUTING.md).

## Commitlint

[Commitlint](https://commitlint.js.org/) is a tool for linting commit messages, giving you feedback on whether the commit follows Conventional Commits' rules and what to change. This tool can be used in the terminal, integrated into your IDE, and added to your CI/CD. A key use case is to stop a commit from progressing if the message is not formatted correctly.

Integration with your IDE (recommended, if you do not use the terminal to edit commits) may require a 3rd-party extension, as this can give linting feedback as you type, rather than executing a commit and receiving an error message whilst it is processing the commit. Providing a list of IDEs and extensions is out of the scope of this demo.

> [!TIP]
> Identify compatible IDE extensions by searching for IDE extensions with the search terms "commitlint" or "conventional commits".

This repository has tested commitlint with VS Code and added an example extension to the [extensions.json recommendations](./.vscode/extensions.json): [vscode-commitlint](https://www.joshbolduc.net/projects/vscode-commitlint).

> [!TIP]
> To open the full commit message editor in VS Code, [keep the commit message text field empty then click on the commit button](https://code.visualstudio.com/docs/sourcecontrol/overview#_author-commit-messages-using-an-editor)&mdash;this will open the commit message editor.

Install commitlint and any IDE extensions:

- If commitlint is already added to a repository you are cloning (such as this demo), it will be added as a project dependency. In this demo, that means you should simply install the dependencies with `npm install` (or `npm i`).
- If you are installing it in a project that has not yet configured it, follow the [commitlint's installation instructions](https://commitlint.js.org/guides/getting-started.html). This will include steps to install [git hooks](#git-hooks) to activate commitlint when a commit message is being edited.

> [!NOTE]
> Commitlint installed in your development environment will not stop collaborators from committing un-conventional commits (commitlint needs to be installed and can be bypassed). If you desire to enforce this, you can explore [configuring a CI workflow](https://commitlint.js.org/guides/ci-setup.html).

Commitlint uses a [commitlint configuration file](./commitlint.config.js). This demo uses the default, but it can be [configured](https://commitlint.js.org/reference/configuration.html).

### Git Hooks

To ensure tools such as commitlint run automatically, git hooks are required. Git hooks are scripts that Git executes before or after events such as: commit, push, and receive. They are a built-in feature of Git and they are used to automate tasks and enforce policies.

In the context of commitlint, a `commit-msg` hook is used. This hook is triggered during the commit process and it's where commitlint checks the commit message for compliance with the rules.

The installation and [setup of this hook are covered in the commitlint's installation instructions](https://commitlint.js.org/guides/local-setup.html#add-hook). It is important to follow these instructions to ensure that the hook is properly configured and working as expected. If the hook is not configured correctly, then commitlint will not automatically run. You can see a simple definition of the hook used in this demo in the [`./.husky/` folder](./.husky/).

> [!NOTE]
> When installing commitlint, following their install guides, it automatically created a `./.husky/pre-commit` hook that ran `npm test`. This was an autogenerated hook (an example hook, essentially). As no tests were defined in this demo project, the commits would fail. If you have a similar situation, you may need to delete any default example hooks located in `./.husky/`.

## Semantic Release

1. [Install Semantic Release](https://semantic-release.gitbook.io/semantic-release/usage/installation).
2. [Configure the CI workflow](https://semantic-release.gitbook.io/semantic-release/usage/ci-configuration)
   - [Common CI configurations](https://semantic-release.gitbook.io/semantic-release/recipes/ci-configurations) are provided.
3. Create a [release config](https://semantic-release.gitbook.io/semantic-release/usage/configuration)

> [!NOTE]
> Semantic Release ships with [default plugins](https://semantic-release.gitbook.io/semantic-release/usage/plugins#default-plugins) enabled by default. Specifying plugins in the config will override the defaults, for example:
>
> ```json
> "plugins": [
>     "@semantic-release/commit-analyzer",
>     "@semantic-release/release-notes-generator",
>     "@semantic-release/github"
>   ]
> ```

Once set up, test everything is installed and configured by performing a dry-run test:

```zsh
npx semantic-release --dry-run
```
