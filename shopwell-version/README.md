# Shopwell Version

Gets the Shopwell version that matches the current branch.

## What it does

1. Finds a matching Shopwell version based on the current git reference
2. Returns a fallback version if no matching branch is found
3. Useful for testing against specific Shopwell versions

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `fallback` | The fallback version if there's no matching branch | No | `trunk` |
| `repo` | The repo where to look for matching refs | No | `shopwell-shop/shopwell` |
| `ref` | The git reference to match (defaults to `github.ref`) | No | - |
| `base-ref` | The base reference for pull requests (defaults to `github.base_ref`) | No | - |
| `head-ref` | The head reference for pull requests (defaults to `github.head_ref`) | No | - |
| `github-token` | GitHub token used to authenticate gh API calls | No | `${{ github.token }}` |

## Outputs

| Output | Description |
|--------|-------------|
| `shopwell-version` | The matching shopwell version or fallback |

## Usage

### Basic usage

```yaml
- uses: shopwell-shop/github-actions/shopwell-version@main
  id: version
```

### With custom fallback

```yaml
- uses: shopwell-shop/github-actions/shopwell-version@main
  id: version
  with:
    fallback: 6.5.0.0
```

### With custom repository

```yaml
- uses: shopwell-shop/github-actions/shopwell-version@main
  id: version
  with:
    repo: my-org/shopwell
    fallback: trunk
    github-token: ${{ secrets.SHOPWELL_TOKEN }}
```

### Using the output

```yaml
- uses: shopwell-shop/github-actions/shopwell-version@main
  id: version
- name: Use version
  run: echo "Shopwell version is ${{ steps.version.outputs.shopwell-version }}"
```
