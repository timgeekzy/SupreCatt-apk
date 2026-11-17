# SupreCart download page

Static page where University of Ilorin students get the **SupreCart** app.
It shows the version and size, links to the app stores and the WhatsApp community.

Plain HTML/CSS/JS with no build step. Push to `main` and the host serves it.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The download page. App details are in the `CONFIG` object near the bottom. |
| `open-shop.html` | Small deep-link handler for `/shop/<id>` links that open a shop in the app. |
| `_redirects` | Routes `/shop` and `/shop/*` to `open-shop.html` (Cloudflare Pages / Netlify). |
| `README.md` | This file. |

## Updating app details

Update `CONFIG` in `index.html`:

```js
var CONFIG = {
  playStoreUrl: "https://play.google.com/store/apps/details?id=...",
  appStoreUrl: "",
  version: "X.Y.Z",
  size: "NN MB",
  whatsappUrl: "https://chat.whatsapp.com/..."
};
```

Open the live page and confirm the version, size and store links match.

## Local preview

```sh
python -m http.server 8000
```

Open <http://localhost:8000>. `_redirects` is not applied locally, so test the deep-link
page directly at `/open-shop.html?seller=123`.

## Notes

- `/shop/<id>` links open `suprecart://shop/<id>`, or an Android intent for package
  `com.suprecart.suprecart`. Update `PACKAGE` in `open-shop.html` if the app id changes.
