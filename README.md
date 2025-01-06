# Theos

Use Theos in your GitHub Actions to build iOS tweaks, even without a Mac.

## Usage
Only macOS runners are supported as of right now

```yaml
- uses: waruhachi/theos-action@v1.0.0
  with:
      # Directory to install Theos to
      theos-dir: '${{ github.workspace }}/theos'
      # What repo to clone Theos from
      theos-src: 'theos/theos'
      # What branch to clone Theos from
      theos-branch: 'master'
      # Cache Theos
      theos-cache: true
      # Directory to cache Theos to
      theos-cache-dir: '${{ github.workspace }}/cache/theos'
      # Directory to install iOS SKs to
      theosSDK-dir: '${{ github.workspace }}/theos/sdks'
      # What repo to clone iOS SKs from
      theosSDK-src: 'theos/sdks'
      # What branch to clone iOS SKs from
      theosSDK-branch: 'master'
      # Cache iOS SDKs
      theosSDK-cache: true
      # Directory to cache iOS SDKs to
      theosSDK-cache-dir: '${{ github.workspace }}/cache/theosSDK'
```
