# SupreCart download & guide page

Static page where University of Ilorin students get the **SupreCart** app and learn
how it works: overview, roles, money flow, features and screenshot guides.

Plain HTML/CSS/JS with no build step. Push to `main` and the host serves it.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The landing + guide page. App details are in the `CONFIG` object near the bottom. |
| `open-shop.html` | Small deep-link handler for `/shop/<id>` links that open a shop in the app. |
| `_redirects` | Routes `/shop` and `/shop/*` to `open-shop.html` (Cloudflare Pages / Netlify). |
| `images/` | Screenshots used by the guides. Add new files here. |
| `README.md` | This file. |

## Page sections (`index.html`)

1. **Hero** — headline, store buttons, version/size, share.
2. **Overview** (`#overview`) — what SupreCart is, categories, payments, trust.
3. **Who it's for** (`#who`) — buyers, sellers, riders & staff.
4. **How it works** (`#how`) — buying and selling flows, delivery, safety.
5. **Features** (`#features`) — chat, payments, reviews, wishlist, payouts, etc.
6. **Guides** (`#guides`) — four walkthroughs (list, buy, sell, chat/track).
7. **FAQ** (`#faq`) + **CTA** — WhatsApp community.

## Adding images

Every image slot is a `<figure class="shot">` with a `data-slot` label naming the
expected file. If the file is missing, the slot shows a dashed placeholder with
that path. Drop the file into `images/` with the exact name and refresh — no HTML
edit needed.

| Slot | File under `images/` |
| --- | --- |
| Overview screenshot | `home.jpg` ✓ |
| Seller dashboard | `seller_dashboard.jpg` ✓ |
| Rider / logistics view | `logistics.jpg` ✓ |
| Buy guide — find item | `search.jpg` ✓ |
| Buy guide — pay | `checkout.jpg` ✓ |
| Buy guide — confirm receipt | `order_details1.jpg` ✓ |
| Sell guide — open shop | `open_shop.jpg` ✓ |
| Sell guide — orders | `order_list.jpg` ✓ |
| Sell guide — payouts | `payout.jpg` ✓ |
| Chat thread | `live_chat.jpg` ✓ |
| Order tracking | `order_tracking.jpg` ✓ |
| Share shop link | `shop_share.jpg` ✓ |

Already present (listing guide): `1.jpeg`, `2.jpeg`, `3.jpeg`.
Also on disk (unused): `order_details2.jpg`.
✓ = wired into the page. All guide slots are filled.

Prefer `.jpeg` / `.jpg` / `.png`. Keep screenshots under ~300 KB so the page stays
fast on mobile data.

To remove a slot entirely, delete its `<figure class="shot" …>…</figure>` block.

## Updating app details

Update `CONFIG` in `index.html`:

```js
var CONFIG = {
  playStoreUrl: "https://play.google.com/store/apps/details?id=...",
  appStoreUrl: "",
  whatsappUrl: "https://chat.whatsapp.com/..."
};
```

Empty store URLs show a **Coming soon** toast on click (no dead links).
Social links (website, Instagram, TikTok, X) are plain anchors in the CTA and footer.

Open the live page and confirm the store links and socials match.

## Local preview

```sh
python -m http.server 8000
```

Open <http://localhost:8000>. `_redirects` is not applied locally, so test the deep-link
page directly at `/open-shop.html?seller=123`.

## Notes

- `/shop/<id>` links open `suprecart://shop/<id>`, or an Android intent for package
  `com.suprecart.suprecart`. Update `PACKAGE` in `open-shop.html` if the app id changes.
- Carousels are generic: any `.carousel` with a `[data-carousel]` track and sibling
  `[data-prev]` / `[data-next]` / `[data-dots]` controls wires itself up in the script.
