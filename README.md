# Theos

Use Theos in your GitHub Actions to build iOS tweaks, even without a Mac.

### Usage

Currently, **only macOS runners** are supported.

### Configuration

The following inputs are available (all are optional) with their default values:

```yaml
- uses: waruhachi/theos-action@v2.3.4
  with:
      theos-src: 'theos/theos'
      theos-branch: 'master'
      theos-dir: '~/theos'
      sdks-src: 'theos/sdks'
      sdks-branch: 'master'
      libgcuniversal: true
      libgcuniversal-src: 'MrGcGamer/LibGcUniversalDocumentation'
      libgcuniversal-branch: 'master'
      altlist: true
      altlist-src: 'opa334/AltList'
      altlist-branch: 'main'
```

-   **`theos-src`**: Repository to clone Theos from.
-   **`theos-branch`**: Branch to clone Theos from.
-   **`theos-dir`**: Directory to clone Theos to.
-   **`sdks-src`**: Repository to clone patched SDKs from.
-   **`sdks-branch`**: Branch to clone patched SDKs from.
-   **`libgcuniversal`**: Whether to use LibGcUniversal.
-   **`libgcuniversal-src`**: Repository to clone LibGcUniversal from.
-   **`libgcuniversal-branch`**: Branch to clone LibGcUniversal from.
-   **`altlist`**: Whether to use AltList.
-   **`altlist-src`**: Repository to clone AltList from.
-   **`altlist-branch`**: Branch to clone AltList from.

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
              uses: waruhachi/theos-action@v2.3.3
              env:
                GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
              with:
                theos-src: 'waruhachi/theos'
                theos-branch: 'main'
                sdks-src: 'waruhachi/sdks'
                sdks-branch: 'main'
                libgcuniversal: 'true'
                libgcuniversal-src: 'waruhachi/LibGcUniversal'
                libgcuniversal-branch: 'main'
                altlist: 'true'
                altlist-src: 'waruhachi/AltList'
                altlist-branch: 'main'

            - name: Build tweak
              run: |
                make clean package FINALPACKAGE=1
                make clean package FINALPACKAGE=1 THEOS_PACKAGE_SCHEME=rootless
                make clean package FINALPACKAGE=1 THEOS_PACKAGE_SCHEME=roothide
```
