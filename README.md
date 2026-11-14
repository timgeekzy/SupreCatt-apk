# SupreCart Android download page

Static page where University of Ilorin students download the **SupreCart** Android APK.
It explains how to sideload the app, shows the version, size and SHA-256 checksum, and
links to the WhatsApp community.

Plain HTML/CSS/JS with no build step. Push to `main` and the host serves it.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The download page. App details are in the `CONFIG` object near the bottom. |
| `open-shop.html` | Small deep-link handler for `/shop/<id>` links that open a shop in the app. |
| `_redirects` | Routes `/shop` and `/shop/*` to `open-shop.html` (Cloudflare Pages / Netlify). |
| `README.md` | This file. |

## Publishing a new APK

1. Upload the APK as a GitHub Release asset and note its tag and size.
2. Get the checksum:
   ```sh
   sha256sum SupreCart-arm64-v8a.apk
   ```
3. Update `CONFIG` in `index.html`:
   ```js
   var CONFIG = {
     apkUrl: "https://github.com/timgeekzy/SupreCatt-apk/releases/download/vX.Y.Z/SupreCart-arm64-v8a.apk",
     version: "X.Y.Z",
     size: "NN MB",
     sha256: "sha256:<hex digest>",
     whatsappUrl: "https://chat.whatsapp.com/..."
   };
   ```
4. Open the live page and confirm the version, size and checksum match.

If `apkUrl` is empty, the download buttons disable themselves and show "Download link
coming soon".

## Local preview

```sh
python -m http.server 8000
```

Open <http://localhost:8000>. `_redirects` is not applied locally, so test the deep-link
page directly at `/open-shop.html?seller=123`.

## Notes

- Android only; the app is distributed as an APK (sideload) until it reaches the Play Store.
- The `download` attribute is ignored for cross-origin URLs, so the file keeps its release-asset name.
- `/shop/<id>` links open `suprecart://shop/<id>`, or an Android intent for package
  `com.suprecart.suprecart`. Update `PACKAGE` in `open-shop.html` if the app id changes.
