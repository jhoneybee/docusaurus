---
id: commands
title: CLI Commands
---

Docusaurus provides a set of scripts to help you generate, serve, and deploy your website. These scripts can be invoked with the `run` command when using Yarn or npm. Some common commands are:

* [`yarn run start`](api-commands.md#docusaurus-start-port-number): build and serve the website from a local server
* [`yarn run examples`](api-commands.md#docusaurus-examples): create example configuration files

## Running from the command line

The scripts can be run using either Yarn or npm. If you've already gone through our Getting Started guide, you may already be familiar with the `start` command. It's the command that tells Docusaurus to run the `docusaurus-start` script which generates the site and starts up a server, and it's usually invoked like so:

```bash
yarn run start
```

The same script can be invoked using npm:

```bash
npm run start
```

To run a particular script, just replace the `start` command in the examples above with the command associated with your script.

## Using arguments

Some commands support optional arguments. For example, to start a server on port 8080, you can specify the `--port` argument when running `start`:

```bash
yarn run start --port 8080
```

If you run Docusaurus using npm, you can still use the command line arguments by inserting a `--` between `npm run <command>` and the command arguments:

```bash
npm run start -- --port 8080
```

## Configuration

These scripts are set up under the `"scripts"` key in your `website/package.json` file as part of the installation process. If you need help setting them up again, please refer to the [Installation guide](getting-started-installation.md).

Docusaurus provides some default mappings to allow you to run commands following Node conventions. Instead of typing `docusaurus-start` every time, you can type `yarn run start` or `npm start` to achieve the same.

## Commands

<AUTOGENERATED_TABLE_OF_CONTENTS>

---

## Reference

### `docusaurus-build`

Alias: `build`.

| Options                    | Default | Description                                                                                                           |
| -------------------------- | ------- | --------------------------------------------------------------------------------------------------------------------- |
| `--skip-image-compression` | `false` | Skip compression of image assets. You usually won't want to skip this unless your images have already been optimized. |
| `--skip-next-release` | `false` | Skip the next release documents when versioning is enabled. This will not build HTML files for documents in `/docs` directory.|

Generates the static website, applying translations if necessary. Useful for building the website prior to deployment.

See also [`docusaurus-start`](api-commands.md#docusaurus-start).

---

### `docusaurus-examples`

Alias: `examples`

| Arguments   | Default | Description                                                                                          |
| ----------- | ------- | ---------------------------------------------------------------------------------------------------- |
| `<feature>` | -       | Specify a feature `translations` or `versions` to generate the extra example files for that feature. |

**Example**

```bash
docusaurus-examples <feature>
```

When no feature is specified, sets up a minimally configured example website in your project. This command is covered in depth in the [Site Preparation guide](getting-started-preparation.md).

---

### `docusaurus-publish`

Alias: `publish-gh-pages`

[Builds](api-commands.md#docusaurus-build), then deploys the static website to GitHub Pages. This command is meant to be run during the deployment step in CircleCI, and therefore expects a few environment variables to be defined:

The following environment variables are generally set manually by the user in the CircleCI `config.yml` file.

* `GIT_USER`: The git user to be associated with the deploy commit.
* `USE_SSH`: Whether to use SSH instead of HTTPS for your connection to the GitHub repo.

**Example**

```bash
GIT_USER=docusaurus-bot USE_SSH=true yarn run publish-gh-pages
```

The following environment variables are [set by CircleCI](https://circleci.com/docs/1.0/environment-variables/) during the build process.

* `CIRCLE_BRANCH`: The git branch associated with the commit that triggered the CI run.
* `CI_PULL_REQUEST`: Expected to be truthy if the current CI run was triggered by a commit in a pull request.

The following should be set by you in `siteConfig.js` as `organizationName` and `projectName`, respectively. If they are not set in your site configuration, they fall back to the [CircleCI environment](https://circleci.com/docs/1.0/environment-variables/).

* `CIRCLE_PROJECT_USERNAME`: The GitHub username or organization name that hosts the Git repo, e.g. "facebook".
* `CIRCLE_PROJECT_REPONAME`: The name of the Git repo, e.g. "Docusaurus".

You can learn more about configuring automatic deployments with CircleCI in the [Publishing guide](getting-started-publishing.md).

---

### `docusaurus-rename-version`

Alias: `rename-version`

Renames an existing version of the docs to a new version name.

| Arguments          | Default | Description               |
| ------------------ | ------- | ------------------------- |
| `<currentVersion>` | -       | Version to be renamed.    |
| `<newVersion>`     | -       | Version to be renamed to. |

**Example**

```bash
docusaurus-rename-version <currentVersion> <newVersion>
```

See the [Versioning guide](guides-versioning.md#renaming-existing-versions) to learn more.

---

### `docusaurus-start`

Alias: `start`.

This command will build the static website, apply translations if necessary, and then start a local server.

| Options           | Default | Description                                                                                                                          |
| ----------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `--port <number>` | `3000`  | The website will be served from port 3000 by default, but if the port is taken up, Docusaurus will attempt to find an available one. |
| `--watch` | -  | Whether to watch the files and live reload the page when files are changed. Defaults to true. Disable this by using `--no-watch`. |

You can specify the browser application to be opened by setting the `BROWSER` environment variable before the command, e.g.:

```
$ BROWSER=firefox yarn start
```

---

### `docusaurus-version <version>`

Alias: `version`

Generates a new version of the docs. This will result in a new copy of your site being generated and stored in its own versioned directory. Useful for capturing snapshots of API docs that map to specific versions of your software. Accepts any string as a version number.

See the [Versioning guide](guides-versioning.md) to learn more.

---

### `docusaurus-write-translations`

Alias: `write-translations`

Writes the English for any strings that need to be translated into an `website/i18n/en.json` file. The script will go through every file in `website/pages/en` and through the `siteConfig.js` file and other config files to fetch English strings that will then be translated on Crowdin. See the [Translation guide](guides-translation.md) to learn more.