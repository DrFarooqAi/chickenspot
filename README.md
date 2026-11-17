# بقعة الدجاج | Chicken Spot

A one-page website for a broast chicken shop, which customers can also install as an app. Customers browse the menu, then send their order to the shop on WhatsApp. No server, database or monthly fees are needed: it runs free on GitHub Pages.

**Live site:** https://drfarooqai.github.io/chickenspot/

---

## What customers get

- **Menu with prices.** They tap + and − to choose quantities, and the total updates as they go.
- **Order on WhatsApp.** The order button opens WhatsApp with the full order already written, including items, total, pickup or delivery, their name, and their location or address. Payment is on pickup or delivery.
- **Open / Closed badge.** It changes on its own based on the shop's hours.
- **Quick buttons.** Directions in Google Maps, call the shop, opening hours, and share the page with friends.
- **Social links.** Instagram, Snapchat and TikTok buttons appear only if the shop has them.
- **Arabic and English.** Arabic is the default, and one tap switches to English.
- **Installable app.** On Android, the **Install** button adds it to the home screen straight away. On iPhone, it shows how to use Share → **Add to Home Screen**. It then opens full-screen with the shop's own icon.
- **Remembers them.** Their name and language are saved for the next order.
- **Works offline.** After the first visit, the page still opens without internet. Sending the order still needs WhatsApp to be online.

---

## Files

| File | What it does |
|---|---|
| `index.html` | The whole website: design, menu, ordering and the **SHOP SETTINGS** block |
| `manifest.webmanifest` | The app's install details: name, colours and icons |
| `sw.js` | The offline helper, which keeps a copy of the page on the phone |
| `icon-192.png`, `icon-512.png` | App icons for Android and the install screen |
| `apple-touch-icon.png` | App icon for iPhone home screens |

---

## How to change the shop details

Open `index.html` and find the block marked **SHOP SETTINGS**. It's near the bottom of the file. **Change only this block.** Everything else stays the same.

```js
const SHOP = {
  name_ar: "بقعة الدجاج",
  name_en: "Chicken Spot",
  whatsapp: "966500000000",                 // shop WhatsApp, international format, no + or spaces
  phone: "+966500000000",
  map: "https://maps.google.com/?q=Riyadh", // paste the shop's Google Maps share link
  area_ar: "الرياض", area_en: "Riyadh",
  open: 12, close: 1,                       // opening hours, 24h clock (close after midnight is fine)
  instagram: "", snapchat: "", tiktok: "",  // optional full links
  items: [
    { id:"p4", pieces:4, ar:"٤ قطع", en:"4 Pieces", sub_ar:"وجبة فردية مع البطاطس", sub_en:"Single meal with fries", price:20 },
    { id:"p8", pieces:8, ar:"٨ قطع", en:"8 Pieces", sub_ar:"وجبة عائلية مع البطاطس", sub_en:"Family meal with fries", price:30, best:true }
  ]
};
```

| Setting | How to fill it |
|---|---|
| `name_ar`, `name_en` | Shop name in Arabic and English |
| `whatsapp` | WhatsApp number where orders arrive, e.g. `966512345678`. Start with 966 and drop the leading 0, with no `+` and no spaces |
| `phone` | Number for the Call button, e.g. `+966512345678` |
| `map` | In Google Maps, open the shop, tap **Share**, copy the link and paste it here |
| `area_ar`, `area_en` | District or city shown under the name |
| `open`, `close` | Hours on a 24-hour clock. `12` means noon and `1` means 1 AM. A closing time after midnight works |
| `instagram`, `snapchat`, `tiktok` | Full profile links. Leave `""` to hide the button |
| `items` | One line per menu item. `price` is in riyals. Add `best:true` to show the "Best seller" tag on one item. Each `id` must be different |

**To add a menu item,** copy an item line, put a comma after the line before it, and change the `id`, names, description and price.

### Changing the app name or colours

The installed app's name and colours are set in `manifest.webmanifest`. Update `name` and `short_name` there to match the shop. `short_name` is the label under the home-screen icon, so keep it short.

### Changing the icon

Replace the three PNG files with the new shop's logo. **Keep the same file names and sizes:** 192×192, 512×512 and 180×180 for `apple-touch-icon.png`. Use a square image with the logo in the middle and some space around it.

---

## How to update the live site

**With GitHub Desktop (easiest):**

1. Edit the files in the `chickenspot` folder on your computer.
2. Open GitHub Desktop. The changed files appear on the left.
3. Type a short summary, such as `Update WhatsApp number`, then click **Commit to main**.
4. Click **Push origin**.
5. The live site updates within 1–2 minutes.

**On the GitHub website:** open the file, click the ✏️ pencil, make the change, then click **Commit changes**.

Customers who installed the app get the new version the next time they open it with internet.

---

## How to make a site for a new shop

1. Copy the whole `chickenspot` folder and rename it, e.g. `albaik-olaya`. Delete the hidden `.git` folder inside the copy.
2. Edit the **SHOP SETTINGS** block in `index.html`.
3. Update the name in `manifest.webmanifest` and the `<title>` at the top of `index.html`.
4. Replace the three icon files.
5. In GitHub Desktop, choose **File → Add local repository**, pick the new folder, and choose **create a repository** if asked.
6. Click **Publish repository**. **Untick "Keep this code private"**, because free GitHub Pages needs a public repository.
7. On GitHub, open the repository's **Settings → Pages**. Under Branch, choose **main** and **/ (root)**, then **Save**.
8. After about a minute, it's live at `https://drfarooqai.github.io/<folder-name>/`.

---

## QR code and printing

Make the QR code from the live link, **https://drfarooqai.github.io/chickenspot/**, and only after the real WhatsApp number is in place. The link never changes when you update the site, so printed QR codes keep working.

Good places for the QR code: the counter, the shop window, food bags and the receipt.

---

## Testing checklist

Before handing the site to the shop owner:

- [ ] The order button opens WhatsApp **to the shop's real number**
- [ ] Prices and items match the shop's menu
- [ ] The Directions button opens the right place in Google Maps
- [ ] The Call button dials the right number
- [ ] The Open / Closed badge is right for the current time
- [ ] The Install button works on Android, and Add to Home Screen works on iPhone
- [ ] Arabic and English both read correctly

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Changes don't show on the live site | Wait 2 minutes, then refresh. On a phone, close and reopen the app |
| WhatsApp opens to the wrong number | Check `whatsapp` in SHOP SETTINGS: digits only, starting with 966, no leading 0 |
| No Install button on iPhone | Normal for iPhone. Use Safari → Share → **Add to Home Screen** |
| Site shows "404" | Check **Settings → Pages** is set to the **main** branch and that the repository is **Public** |
| Page looks broken after an edit | A comma or quote is probably missing in SHOP SETTINGS. Compare with the example above |

---

## Current status

- ✅ Live on GitHub Pages
- ⚠️ **The WhatsApp number and phone are still placeholders** (`966500000000`). Replace them before printing the QR code.
- ⚠️ The map link points to Riyadh in general. Replace it with the shop's exact Google Maps link.
