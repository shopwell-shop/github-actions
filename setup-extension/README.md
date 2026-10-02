# Setup Extension

Checkouts Shopwell and extension, optionally installs dependencies and sets up the database.

## What it does

1. Determines the Shopwell version to use
2. Sets up Shopwell using the shopwell-shop/setup-shopwell action
3. Clones the extension (or downloads from an artifact)
4. Handles both plugins and apps
5. Installs extension dependencies
6. Optionally installs Shopwell, admin, and storefront dependencies

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `extensionName` | Your extension name | Yes | - |
| `extensionRef` | The branch/tag to checkout | No | - |
| `shopwellVersion` | Shopwell version (`.auto` to auto-detect) | No | `.auto` |
| `shopwellVersionFallback` | Fallback version | No | `trunk` |
| `shopwell-repository` | The shopwell repository to checkout | No | `shopwell-shop/shopwell` |
| `shopwell-github-token` | Token for checking out shopwell repository | No | `$GITHUB_TOKEN` |
| `phpVersion` | PHP version to use | No | `8.2` |
| `mysqlVersion` | Mysql image to use or `builtin` | No | `builtin` |
| `node-version` | Node.js version to use | No | `20.x` |
| `npm-version` | NPM version to use | No | - |
| `composerRootVersion` | The COMPOSER_ROOT_VERSION | No | `.auto` |
| `dependencies` | JSON list defining dependencies | No | - |
| `extraRepositories` | Additional composer repositories | No | `{}` |
| `install` | Whether to install Shopwell | No | - |
| `install-admin` | Whether to install admin npm deps | No | - |
| `install-storefront` | Whether to install storefront npm deps | No | - |
| `skip-js-build` | Skip js build step | No | `false` |
| `env` | Environment for Shopwell | No | `test` |
| `keep-composer-tools` | Keep Shopwell Composer tools | No | `false` |
| `extension-zip` | Artifact (extension zip) to download | No | - |
| `with-submodules` | Checkout with submodules | No | `false` |
| `allow-insecure-versions` | Allow older Shopwell versions with vulnerabilities | No | `false` |

## Usage

### Basic usage

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: shopwell-shop/github-actions/setup-extension@main
        with:
          extensionName: MyExtensionName
          shopwell-github-token: ${{ secrets.GITHUB_TOKEN }}
```

### With installation

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: shopwell-shop/github-actions/setup-extension@main
        with:
          extensionName: MyExtensionName
          install: 'true'
          install-admin: 'true'
          shopwell-github-token: ${{ secrets.GITHUB_TOKEN }}
```

### With dependencies

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: shopwell-shop/github-actions/setup-extension@main
        with:
          extensionName: MyExtensionName
          install: 'true'
          dependencies: |-
            [
              {"name": "SwagPlatformDemoData", "repo": "git@github.com:shopwell/SwagPlatformDemoData.git"}
            ]
          shopwell-github-token: ${{ secrets.GITHUB_TOKEN }}
```

### With custom Shopwell version

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: shopwell-shop/github-actions/setup-extension@main
        with:
          extensionName: MyExtensionName
          shopwellVersion: 6.5.x
          shopwell-github-token: ${{ secrets.GITHUB_TOKEN }}
```

### From extension zip artifact

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Build zip
        run: ./build-zip.sh
      - uses: actions/upload-artifact@v4
        with:
          name: my-extension
          path: my-extension.zip

  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: shopwell-shop/github-actions/setup-extension@main
        with:
          extensionName: MyExtensionName
          extension-zip: my-extension
          install: 'true'
          shopwell-github-token: ${{ secrets.GITHUB_TOKEN }}
```

### With additional composer repositories

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: shopwell-shop/github-actions/setup-extension@main
        with:
          extensionName: MyExtensionName
          extraRepositories: |-
            {
              "customRepo": {
                "type": "vcs",
                "url": "https://my-custom-repo.example.test/foo/bar.git"
              }
            }
          shopwell-github-token: ${{ secrets.GITHUB_TOKEN }}
```

### With private dependencies

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: shopwell-shop/github-actions/setup-extension@main
        with:
          extensionName: MyExtensionName
          install: 'true'
          dependencies: |-
            [
              {"name": "MyPrivateExtension", "repo": "https://user:$MY_EXTENSION_TOKEN@gitlab.domain.com/org/my-extension.git"}
            ]
          shopwell-github-token: ${{ secrets.GITHUB_TOKEN }}
```

## Requirements

- GitHub token with `repo` permissions
- For private dependencies, store tokens as repository secrets
