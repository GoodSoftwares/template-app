# GoodSoftware Template

A reusable GitHub Actions template: periodically / manually checks whether the source site's APK has been updated. Once a change is detected, it automatically calculates the SHA256, creates a Release, and updates the download page and version history.

## How It Works

1. Download the latest APK from `APK_URL`, calculate its SHA256, and compare it with the last recorded value (`last_hash.txt`).
2. If the hash is unchanged → do nothing; if it has changed → use `aapt` to read the `versionName`.
3. Append a record to `history.csv`, regenerate the `docs/index.md` download page, and create a Release with the APK attached.
4. Commit `last_hash.txt` / `history.csv` / `docs/index.md` back to the repository.

## Quick Start

You can directly edit the two variables under `env:` at the top of `.github/workflows/release.yml`:

```yaml
env:
  APP_NAME: "YourAppName"
  APK_URL: "https://your.app/download/url.apk"
```

Then push to the `main` branch (or manually run the workflow from the Actions page) to run it automatically.

## Optional: Enable the Download Page

After `docs/index.md` is generated, you can enable GitHub Pages to display it: **Settings → Pages → Source select `Deploy from a branch` → select branch `main`, directory `/docs`**.
