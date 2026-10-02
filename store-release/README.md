# Store Release

Builds the extension and uploads a zip of it to the Shopwell Store.

## What it does

1. Builds the extension zip
2. Validates the zip (built-in checks, `--only sw-cli`)
3. Uploads to Shopwell Store
4. Optionally creates a GitHub release
5. Optionally creates a git tag

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `extensionName` | Your extension name | Yes | - |
| `publishOnly` | Publish only to Shopwell Store and don't create a tag | No | `false` |
| `path` | Path to your bundle | No | `.` |
| `clientId` | Your Shopwell account client ID for API authentication | No* | - |
| `clientSecret` | Your Shopwell account client secret for API authentication | No* | - |
| `accountUser` | Your Shopwell account user (deprecated) | No* | - |
| `accountPassword` | Your Shopwell account password (deprecated) | No* | - |
| `ghToken` | GitHub token | Yes | - |
| `skipCheckout` | Skip the checkout step | No | `false` |
| `disableGit` | Use the source folder as it is | No | `false` |
| `updateInfo` | Update extension information on the Shopwell Store plugin page | No | `false` |

*\* Either `clientId`/`clientSecret` or `accountUser`/`accountPassword` must be provided.*

## Usage

### Basic usage (client credentials)

```yaml
name: Release to Store

on:
  workflow_dispatch:

jobs:
  build:
    uses: shopwell-shop/github-actions/store-release@main
    with:
      extensionName: MyExtensionName
      clientId: ${{ secrets.SHOPWELL_CLIENT_ID }}
      clientSecret: ${{ secrets.SHOPWELL_CLIENT_SECRET }}
      ghToken: ${{ secrets.GITHUB_TOKEN }}
```

### Basic usage (legacy username/password)

```yaml
name: Release to Store

on:
  workflow_dispatch:

jobs:
  build:
    uses: shopwell-shop/github-actions/store-release@main
    with:
      extensionName: MyExtensionName
      accountUser: ${{ secrets.SHOPWELL_ACCOUNT_USER }}
      accountPassword: ${{ secrets.SHOPWELL_ACCOUNT_PASSWORD }}
      ghToken: ${{ secrets.GITHUB_TOKEN }}
```

### Publish only (no GitHub release)

```yaml
jobs:
  build:
    uses: shopwell-shop/github-actions/store-release@main
    with:
      extensionName: MyExtensionName
      publishOnly: 'true'
      clientId: ${{ secrets.SHOPWELL_CLIENT_ID }}
      clientSecret: ${{ secrets.SHOPWELL_CLIENT_SECRET }}
      ghToken: ${{ secrets.GITHUB_TOKEN }}
```

### Update extension info

```yaml
jobs:
  build:
    uses: shopwell-shop/github-actions/store-release@main
    with:
      extensionName: MyExtensionName
      updateInfo: 'true'
      clientId: ${{ secrets.SHOPWELL_CLIENT_ID }}
      clientSecret: ${{ secrets.SHOPWELL_CLIENT_SECRET }}
      ghToken: ${{ secrets.GITHUB_TOKEN }}
```

## Requirements

- Shopwell account credentials must be stored as secrets. Either:
  - `SHOPWELL_CLIENT_ID` and `SHOPWELL_CLIENT_SECRET` (recommended, generate at [Shopwell Account](https://account.shopwell.com/producer/development))
  - `SHOPWELL_ACCOUNT_USER` and `SHOPWELL_ACCOUNT_PASSWORD` (deprecated)
- GitHub token with `repo` permissions
