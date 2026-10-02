# npm ci retry

Runs `npm ci` or another install command with three attempts and npm retry settings.

## Usage

```yaml
- uses: shopwell-shop/github-actions/npm-ci-retry@main
  with:
    working-directory: path/to/package
    command: npm ci
```
