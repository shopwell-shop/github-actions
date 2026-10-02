# ESLint

Runs ESLint on the administration or storefront files of a Shopwell extension.

## What it does

1. Clones Shopwell repository
2. Clones your extension
3. Installs npm dependencies
4. Runs the lint command

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `extensionName` | Your extension name | Yes | - |
| `projectPath` | Path to the JS project to be linted | No | `src/Resources/app/administration` |
| `npmLintCmd` | The npm command to run | No | `lint` |
| `shopwellVersion` | Shopwell version (`.auto` to auto-detect) | No | `.auto` |
| `shopwellVersionFallback` | Fallback version in case there's no matching branch | No | `trunk` |
| `shopwell-repository` | The shopwell repository to checkout | No | `shopwell-shop/shopwell` |
| `shopwell-github-token` | Token used for checking out the shopwell repository | No | `$GITHUB_TOKEN` |
| `forceInstallAdminDeps` | Install platform admin deps | No | - |
| `forceInstallStorefrontDeps` | Install platform storefront deps | No | - |

## Usage

### Basic usage (administration)

```yaml
jobs:
  eslint:
    uses: shopwell-shop/github-actions/eslint@main
    with:
      extensionName: MyExtensionName
```

### Lint storefront

```yaml
jobs:
  eslint:
    uses: shopwell-shop/github-actions/eslint@main
    with:
      extensionName: MyExtensionName
      projectPath: src/Resources/app/storefront
```

### With custom Shopwell version

```yaml
jobs:
  eslint:
    uses: shopwell-shop/github-actions/eslint@main
    with:
      extensionName: MyExtensionName
      shopwellVersion: 6.5.x
```

### With custom repository and token

```yaml
jobs:
  eslint:
    uses: shopwell-shop/github-actions/eslint@main
    with:
      extensionName: MyExtensionName
      shopwell-repository: my-org/shopwell
      shopwell-github-token: ${{ secrets.SHOPWELL_TOKEN }}
```

### With custom lint command

```yaml
jobs:
  eslint:
    uses: shopwell-shop/github-actions/eslint@main
    with:
      extensionName: MyExtensionName
      npmLintCmd: lint:fix
```
