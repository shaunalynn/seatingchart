# Find Your Seat — setup

A single-page seating finder that reads your guest list live from a Google Sheet.
Guests open one link, type their name (typos and partial names are fine), and see their table.

---

## 1. Build the guest list (Google Sheets)

Make a sheet with headers in **row 1**. Only the first two are required:

| Name | Table | Note (optional) | Hint (optional) |
|------|-------|-----------------|-----------------|
| Guest Name 1 | 7 | Right near the dance floor. | |
| Guest Name 2 | 3 | | Bride's side |
| Guest Name 3 | 9 | | Groom's cousin |
| Guest Name 4 | Head Table | With the wedding party. | |

- **Table** can be a number (`7` → shows "TABLE 7") or text (`Head Table` → shows "HEAD TABLE").
- **Note** prints as the small italic line under the table number. Leave blank for none.
- **Hint** only appears when two guests share a name, to help them pick the right row (e.g. "Bride's side"). It is never shown otherwise.

## 2. Publish the sheet as CSV

In the sheet: **File → Share → Publish to web → pick the sheet tab → Comma-separated values (.csv) → Publish.**
Copy the link it gives you (ends in `output=csv`), then open `index.html` and paste it here:

```js
const CONFIG = {
  sheetCsvUrl: "PASTE_YOUR_CSV_LINK_HERE"
};
```

Leave it blank to preview with the built-in sample list.

> **Privacy:** publishing makes that tab's contents (names + tables) readable by anyone who has the CSV link. For a wedding that's usually fine, but if you'd rather the raw sheet not be public, swap to a Google Apps Script Web App that returns only Name/Table — happy to set that up.

## 3. (Optional) Add the floral

Drop your "so very grateful" floral image in this folder named **`floral.jpg`**. Without it, the crown falls back to a dark wash that still looks intentional.

## 4. Deploy

Easiest: go to Netlify → **drag this whole folder onto the deploy area**. You get a public link instantly. Share that link with guests (a QR code on the place cards or invite works well).
No rebuilds needed after that — see below.

---

## Updating on the day

Just edit the Google Sheet. The page re-reads it every time someone loads the link, so changes show up on their own.
One caveat: Google caches the published CSV for **a few minutes**, so a seat change can take ~5 min to propagate — not instant, but fine for day-of tweaks.

## Tweaking the look

Everything is in `index.html`:
- Colors: the `:root` CSS variables (`--olive`, `--cream`, `--terra`, …).
- Display font: set `--display` to your real suite font once it's self-hosted (currently approximated with Italiana).
- Copy: search the file for `We saved you a seat.`, `Let's party.`, and the "can't find that name" line to reword.

## Try it now

Open `index.html` in any browser. With no sheet link set, it runs on the sample list — type "shauna", "maria", or a deliberate typo to feel the matching.
