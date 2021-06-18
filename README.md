# monorepo-publish-example

The purpose of this repo is to demonstrate a minimum working example of publishing to npm with a monorepo on GitHub Actions using Lerna. 

## 📋 Requirements

* Lerna installed
* npm v7+ for package-management
* GitHub repository
* npmjs.com account

## ⚙️ Setup

### 🔑  Create Access Token for npm

An access token is required for publishing to npm with GitHub Actions. You can create a new token by:

1. Login to [npmjs.com](https://npmjs.com)
2. Click on your user icon (upper-right-hand corner)
3. Select "Access Tokens" from the drop-down
4. Click "Generate New Token" button
5. Choose "Automation" from the options
6. Copy the Access Token

### 🤫  Add Secret to Repository

With the access token created for npm, you need to create a "secret" that can be used by GitHub Actions. To add the secret:

1. Click on your repo Settings
2. Choose Secrets on the side menu
3. Click "New Repository Secret" button
4. Enter name: `NPM_TOKEN`
5. Enter value by pasting Access Token
6. Done! 

Now you are ready to publish to npm on GitHub!

## 🏃 Workflow

### 1. Version Bump

In order to publish a new release run `npm run release` locally, this will take you through the Lerna workflow for doing a version bump. Once that's done, your version will get tagged and pushed to GitHub.

### 2. Create Release

From GitHub, create a new release using the existing tag that was pushed.

### 3. Automated Publish

This should kick off the GitHub Actions and publish the result to npm.

## 😈 Gotchas

There are a few small points worth noting about this setup:

* Lerna has a [problem](https://github.com/lerna/lerna/issues/2891) with npm 7+ which doesn't update the lock file, this creates issues on GitHub Actions by having an unclean workspace. To get around this, we manually do the tagging ourselves (see [scripts/tag-release.sh](scripts/tag-release.sh)).
* If using scoped packages, make sure `"publishConfig": { "access": "public" }` is added to each package, as Lerna will assume scoped packages are private by default.

## 🔗 Projects Using This Workflow

* [PixiJS](https://github.com/pixijs/pixijs)
* [PixiJS Filters](https://github.com/pixijs/filters)

