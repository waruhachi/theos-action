# Theos

Use Theos in your GitHub Actions to build iOS tweaks, even without a Mac.

### Usage

Currently, **only macOS runners** are supported.

### Configuration

The following inputs are available (all are optional):

```yaml
- uses: waruhachi/theos-action@v2.3.1
  with:
      theos-dir: '~/theos'
      theos-src: 'theos/theos'
      theos-branch: 'master'
      sdks: true
      sdks-src: 'theos/sdks'
      theos-cache: true
      libgcuniversal: true
      libgcuniversal-src: 'MrGcGamer/LibGcUniversalDocumentation'
      altlist: true
      altlist-src: 'opa334/AltList'
```

-   **`theos-dir`**: Directory to install Theos to.
-   **`theos-src`**: Repository to clone Theos from.
-   **`theos-branch`**: Branch to clone Theos from.
-   **`theos-cache`**: Whether to cache Theos.
-   **`sdks`**: Whether to install custom SDKs.
-   **`sdks-src`**: Repository to clone custom SDKs from.
-   **`libgcuniversal`**: Whether to install LibGcUniversal.
-   **`libgcuniversal-src`**: Repository to clone LibGcUniversal from.
-   **`altlist`**: Whether to install AltList.
-   **`altlist-src`**: Repository to clone AltList from.

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
              uses: waruhachi/theos-action@v2.3.1
              env:
                  GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
              with:
                  theos-src: 'waruhachi/theos'
                  theos-branch: 'main'
                  theos-cache: true
                  sdks: true
                  sdks-src: 'waruhachi/sdks'
                  libgcuniversal: true
                  libgcuniversal-src: 'waruhachi/LibGcUniversal'
                  altlist: true
                  altlist-src: 'waruhachi/AltList'

            - name: Build tweak
              run: |
                  make clean package FINALPACKAGE=1
                  make clean package FINALPACKAGE=1 THEOS_PACKAGE_SCHEME=rootless
                  make clean package FINALPACKAGE=1 THEOS_PACKAGE_SCHEME=roothide
```
