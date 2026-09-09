# Psalm Github Security Scan by and for Mbin

Run [Psalm’s Security Analysis](https://psalm.dev/docs/security_analysis/) as a Github action (a more general version [can be found here](https://github.com/psalm/psalm-github-actions)).

```yaml
name: Psalm Security Scan

on: [push, pull_request]

jobs:
  psalm-security-scan:
    name: Psalm
    runs-on: ubuntu-latest
    permissions:
      contents: read
      security-events: write
    steps:
      - name: Checkout code
        uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1 # v7.0.1

      - name: Psalm Security Scan
        uses: docker://ghcr.io/mbinorg/psalm-security-scan

      - name: Import Security Analysis results into GitHub Security Code Scanning
        uses: github/codeql-action/upload-sarif@fddeee1a7ece751b577e409a89057319e3172939 # v4
        with:
          sarif_file: results.sarif
```

## Specify Psalm version

You can also specify a version.

```diff
-        uses: docker://ghcr.io/mbinorg/psalm-security-scan
+        uses: docker://ghcr.io/mbinorg/psalm-security-scan:5.26.2
```
