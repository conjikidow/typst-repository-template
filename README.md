# typst-repository-template

[![Typst Version](https://img.shields.io/badge/typst-0.12%20%7C%200.13-blue)](https://typst.app/)
[![styled with typstyle](https://img.shields.io/badge/styled_with-typstyle-024a51.svg?style=flat)](https://github.com/typstyle-rs/typstyle)

This is a template repository for Typst projects.

## GitHub Actions Permissions Setup

To enable GitHub Actions to run properly in your repository, you need to adjust the default permissions granted to the `GITHUB_TOKEN`. This is especially important for **private repositories**.

Follow these steps to configure the permissions:

1. Go to the **Settings** tab of your repository.
2. On the left-hand menu, select **Actions/General**.
3. Under the **Workflow permissions** section, ensure the following options are selected:
   - **`Read and write permissions`**: This grants read and write access to the repository for all scopes.
   - **`Allow GitHub Actions to create and approve pull requests`**: This allows GitHub Actions to create pull requests.
4. Save the changes.

![GitHub Actions permissions setup screenshot](https://github.com/user-attachments/assets/da55e896-e087-486e-aadc-7fc1283dc652)

These settings are **necessary only for private repositories**. For public repositories, this configuration is not required.

## CI Setup

The CI workflow compiles the main Typst source file.
You can specify its path in [`ci.yaml`](.github/workflows/ci.yaml#L11):

```yaml
env:
  TYPST_MAIN_FILE: main.typ
```

## Pre-commit Hooks Setup

To enable pre-commit hooks in your repository, you need to install `pre-commit` by running the following command:

```console
uvx pre-commit install
```

The pre-commit hooks also rely on `typstyle` being installed locally. We recommend installing it with `cargo binstall`:

```console
cargo binstall typstyle
```

For other installation methods, please refer to the [official documentation](https://typstyle-rs.github.io/typstyle/installation.html).

## Version Bumping by Labels

This repository is configured to automatically bump the version when a pull request is merged with one of the following labels:

- `update::major`
- `update::minor`
- `update::patch`

Simply add one of these labels to your pull request before merging.
A new pull request for the version bump will be automatically created.

The version number is managed via the `.bumpversion.toml` file in the repository root.
If your project defines its version in specific files (e.g., `typst.toml`, etc.), you may need to add entries like the following to `.bumpversion.toml`:

```toml
[[tool.bumpversion.files]]
filename = "typst.toml"
search = 'version = "{current_version}"'
replace = 'version = "{new_version}"'
```

For more details, see [conjikidow/bump-version](https://github.com/conjikidow/bump-version).
