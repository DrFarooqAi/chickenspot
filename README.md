# بروست د. فاروق الحار | Dr Farooq Spicy Broast

A free ordering website for a broast shop, which customers can also install as an app. Customers choose meals, pick options, review their cart, and send the finished order to the shop on WhatsApp. No server, app store, database or monthly fees are needed: it runs free on GitHub Pages.

**Live site:** https://drfarooqai.github.io/chickenspot/

---

## What customers get

- **Sticky menu tabs.** Deals, Popular, Broast, Sides and Drinks stay at the top while scrolling. The active tab lights up on its own.
- **Deal cards with savings.** Each deal shows a **"Save X SAR"** badge and the crossed-out normal price, worked out automatically from what's inside the deal.
- **Popular tab.** It shows the most-ordered items, marked "🔥 Most ordered".
- **Options pop-up.** Tapping an item opens a sheet where customers choose:
  - the size, such as quarter, half or full broast, with what comes with each
  - **Spicy 🌶 or Regular**
  - extra sauces, such as garlic, hot or cheese, with prices added
  - the quantity, with a live total
- **A proper cart.** Customers review the order, change quantities, remove items, and add a note such as "no garlic sauce".
- **Branch picker.** It appears only when the shop has 2 or more branches. Each branch gets orders on its own WhatsApp.
- **Pickup or delivery.** For delivery, customers send their GPS location or type their area.
- **Reorder in one tap.** After the first order, a "🔁 Reorder your last order" button appears at the top.
- **Remembers them.** The cart, name, address, language and branch are kept, even if they close the app.
- **Open / Closed badge.** If the shop is closed, the cart tells customers the order will be prepared at opening time.
- **Arabic and English.** The site opens in Arabic on Arabic phones and in English on others, and one tap switches. Browser auto-translate is turned off, because it garbles the menu, for example turning "عرض الاثنين" into "Monday Show".
- **Food drawings.** Every item has its own drawing, such as a bucket, burger, fries or drink. Wide screens show the menu as a grid.
- **Installable app.** On Android, the **Install** button adds it to the home screen. On iPhone, customers use Share → **Add to Home Screen**.
- **Works offline.** After the first visit, the menu opens without internet. Sending the order needs WhatsApp to be online.

### What the shop receives on WhatsApp

```
السلام عليكم، أبي أطلب:

• 2 × بروست دجاج (نص · عادي · + صوص ثوم) = 44 ر.س
• 1 × عرض العائلة (حار) = 62 ر.س

*المجموع: 106 ر.س*
نوع الطلب: توصيل
الاسم: محمد
الموقع: https://maps.google.com/?q=24.69,46.68
ملاحظة: بدون صوص ثوم
الدفع عند الاستلام
```

---

## Files

| File | What it does |
|---|---|
| `index.html` | The whole website, including the **SHOP SETTINGS** block with the menu |
| `manifest.webmanifest` | The app's install details: name, colours and icons |
| `sw.js` | The offline helper |
| `icon-192.png`, `icon-512.png` | App icons for Android and the install screen |
| `apple-touch-icon.png` | App icon for iPhone |

---

## How to change the shop and menu

Open `index.html` and find the block marked **SHOP SETTINGS** near the bottom. **Change only this block.** A full new menu takes about 10 minutes.

### Shop details

```js
name_ar: "بروست د. فاروق الحار",
name_en: "Dr Farooq Spicy Broast",
open: 12, close: 1,                        // 24h clock: 12 = noon, 1 = 1 AM
instagram: "", snapchat: "", tiktok: "",   // full links, or "" to hide
```

### Branches

```js
branches: [
  { id:"main", ar:"الفرع الرئيسي", en:"Main branch", area_ar:"الرياض", area_en:"Riyadh",
    whatsapp:"966500000000", phone:"+966500000000", map:"https://maps.google.com/?q=Riyadh" }
]
```

| Field | How to fill it |
|---|---|
| `whatsapp` | The number where orders arrive, e.g. `966512345678`. Start with 966 and drop the leading 0, with no `+` and no spaces |
| `phone` | Number for the Call button, e.g. `+966512345678` |
| `map` | In Google Maps, open the shop, tap **Share**, copy the link and paste it here |

**To add a branch,** copy the branch line, put a comma between the lines, and give it a new `id`. A commented example is already in the file. With 2 or more branches, the branch picker appears in the cart on its own.

### Sauces and categories

```js
sauces: [ { id:"garlic", ar:"صوص ثوم", en:"Garlic sauce", price:2 }, ... ],
categories: [ { id:"deals", ar:"العروض", en:"Deals" }, { id:"broast", ... }, ... ]
```

The **Popular** tab is made automatically. You don't add it to `categories`. A category with no items is hidden.

### Menu items: the 3 kinds

**1. A simple item** has one price and no options. The + button adds it straight to the cart.

```js
{ id:"coleslaw", cat:"sides", art:"coleslaw", ar:"كول سلو", en:"Coleslaw", price:4 }
```

**2. An item with sizes and options:**

```js
{ id:"broast", cat:"broast", art:"broast", ar:"بروست دجاج", en:"Broasted Chicken",
  spicy:true, sauce:true, popular:true,
  sub_ar:"مقرمش من برا وطري من داخل", sub_en:"Crispy outside, juicy inside",
  sizes:[
    { id:"q", ar:"ربع", en:"Quarter", sub_ar:"قطعتين + بطاطس + خبز + صوصين", sub_en:"2 pieces + fries, bun & 2 sauces", price:13 },
    { id:"h", ar:"نص",  en:"Half",    price:20 },
    { id:"f", ar:"كامل", en:"Full",   price:30 }
  ] }
```

**3. A deal** lists what's inside under `includes`. The site adds up those normal prices and shows the saving.

```js
{ id:"family", cat:"deals", art:"bucket", ar:"عرض العائلة", en:"Family Deal", price:62,
  spicy:true, sauce:true, popular:true,
  sub_ar:"بروست كامل + ٢ برجر بروست + بطاطس كبير + مشروب ١ لتر",
  sub_en:"Full broast + 2 broast burgers + large fries + 1L drink",
  includes:["broast:f","burger*2","fries:l","drink:1l"] }
```

`"broast:f"` means the broast item in size `f`. `"burger*2"` means 2 burgers. Here the items are worth 73 SAR, so the card shows **Save 11 SAR**.

| Field | Meaning |
|---|---|
| `id` | A short unique name. It must be different for every item |
| `cat` | Which tab the item appears under: `deals`, `broast`, `sides` or `drinks` |
| `art` | The food drawing on the card: `bucket`, `broast`, `burger`, `strips`, `wings`, `fries`, `coleslaw`, `hummus`, `bun`, `soda`, `water` or `juice` |
| `ar`, `en` | Item name |
| `sub_ar`, `sub_en` | Optional short description |
| `price` | Price in SAR, for items without sizes |
| `sizes` | A list of sizes, each with its own `id` and `price` |
| `spicy:true` | The customer chooses Spicy or Regular. Spicy is selected first |
| `sauce:true` | The customer can add extra sauces |
| `popular:true` | The item also appears in the Popular tab |
| `includes` | For deals only: what's inside, used to work out the saving |

### App name and icon

- The installed app's name is in `manifest.webmanifest`, as `name` and `short_name`. `short_name` is the label under the home-screen icon, so keep it short.
- To change the icon, replace the three PNG files. **Keep the same file names and sizes:** 192×192, 512×512 and 180×180. Keep the logo away from the edges, because Android crops the corners.

---

## How to update the live site

**With GitHub Desktop (easiest):**

1. Edit the files in the `chickenspot` folder on your computer.
2. Open GitHub Desktop. The changed files appear on the left.
3. Type a short summary, such as `Update menu prices`, then click **Commit to main**.
4. Click **Push origin**.
5. The live site updates within a few minutes.

**On the GitHub website:** open the file, click the ✏️ pencil, make the change, then click **Commit changes**.

When you change the site, also raise the number in the first line of `sw.js`, for example `chickenspot-v4` to `chickenspot-v5`. This makes installed apps pick up the new version.

---

## How to make a site for a new shop

1. Copy the whole `chickenspot` folder and rename it, e.g. `albaik-olaya`. Delete the hidden `.git` folder inside the copy.
2. Edit the **SHOP SETTINGS** block in `index.html`: name, branches, hours and menu.
3. Update the name in `manifest.webmanifest` and the `<title>` near the top of `index.html`.
4. Replace the three icon files.
5. In GitHub Desktop, choose **File → Add local repository**, pick the new folder, and choose **create a repository** if asked.
6. Click **Publish repository**.
7. On GitHub, open the repository's **Settings → Pages**. Under Branch, choose **main** and **/ (root)**, then click **Save**.
8. It's live at `https://drfarooqai.github.io/<folder-name>/`.

---

## QR code and printing

Make the QR code from **https://drfarooqai.github.io/chickenspot/**, and only after the real WhatsApp number is in place. The link stays the same when you update the menu, so printed QR codes keep working.

Good places for it: the counter, the shop window, food bags and receipts.

---

## Testing checklist

- [ ] An order sends to WhatsApp **at the shop's real number**
- [ ] Items, sizes, prices and deal savings match the shop's menu
- [ ] Spicy/Regular and the extra sauces appear in the WhatsApp message
- [ ] With more than one branch, each branch receives its own orders
- [ ] The Directions and Call buttons are right
- [ ] The Open / Closed badge is right for the current time
- [ ] Reorder works after the first order
- [ ] The app installs on Android, and Add to Home Screen works on iPhone
- [ ] Arabic and English both read correctly

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Changes don't show | Wait a few minutes and refresh. Raise the version in `sw.js`. On a phone, close and reopen the app |
| WhatsApp opens to the wrong number | Check the branch's `whatsapp`: digits only, starting with 966, no leading 0 |
| The menu is empty or the page is blank | A comma, quote or bracket is missing in SHOP SETTINGS. Compare with the examples above |
| No "Save" badge on a deal | Check that every `includes` entry matches a real item `id` and size `id`, and that the deal price is lower than the total |
| No Install button on iPhone | Normal for iPhone. Use Safari → Share → **Add to Home Screen** |
| Site shows "404" | Check that **Settings → Pages** is set to the **main** branch |

---

## Current status

- ✅ Pro ordering: tabs, options, deals, cart, notes, branches and reorder
- ⚠️ **The WhatsApp number and phone are placeholders** (`966500000000`). Replace them before printing the QR code.
- ⚠️ The map link points to Riyadh in general. Replace it with the shop's exact Google Maps link.
- ⚠️ The menu items and prices are examples. Replace them with the shop's real menu.
