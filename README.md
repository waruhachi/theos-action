# Theos

Use Theos in your GitHub Actions to build iOS tweaks, even without a Mac.

### Usage

Currently, **only macOS runners** are supported.

### Configuration

The following inputs are available (all are optional):

```yaml
- uses: waruhachi/theos-action@v2.1.5
  with:
      theos-dir: '~/theos'
      theos-src: 'theos/theos'
      theos-branch: 'master'
      theos-cache: true
```

-   **`theos-dir`**: Directory to install Theos to.
-   **`theos-src`**: Repository to clone Theos from.
-   **`theos-branch`**: Branch to clone Theos from.
-   **`theos-cache`**: Whether to cache Theos.

---

### Example Workflow

```yaml
name: Build with Theos
on:
    push:
        branches:
            - main

jobs:
    build:
        runs-on: macos-latest

        steps:
            - name: Checkout code
              uses: actions/checkout@v4

            - name: Setup Theos
              uses: waruhachi/theos-action@v2.1.5
              env:
                  GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
              with:
                  theos-src: 'roothide/theos'
                  theos-branch: 'master'
                  theos-cache: true

            - name: Build tweak
              run: |
                  make clean package FINALPACKAGE=1
                  make clean package FINALPACKAGE=1 THEOS_PACKAGE_SCHEME=rootless
                  make clean package FINALPACKAGE=1 THEOS_PACKAGE_SCHEME=roothide
```
