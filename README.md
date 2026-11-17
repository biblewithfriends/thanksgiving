# Thanksgiving Love Feast 2026 — planning site

A site for the church family with five pages (Layout, Invite, Day of, Serve, Dishes): the room map, the invitation list, a day-of checklist, open serving spots, and dishes for Space C and Space D. Everything reads from and writes to the **Thanksgiving Dinner Service Sign Up** Google Sheet.

## Files
- `index.html` — the whole website (put it on GitHub Pages)
- `og-turkey.jpg` and `apple-touch-icon.png` — the turkey picture shown when you text the link, and the home-screen icon. Upload them next to `index.html`.
- `Code.gs` — the Google Apps Script that connects the site to the sheet

## Set up (about 10 minutes)
1. Open the Google Sheet → **Extensions → Apps Script**. Paste `Code.gs` and save.
2. Click **Run → testRead** once and approve the permissions. Check **View → Logs**; you should see the slots and dishes.
3. **Deploy → New deployment → Web app**. Set Execute as **Me** and Who has access **Anyone**. Copy the URL that ends in `/exec`.
4. In `index.html`, paste that URL into `API_URL: ""` near the top.
5. Upload `index.html`, `og-turkey.jpg` and `apple-touch-icon.png` to a GitHub Pages repo named `thanksgiving` (so the site is `biblewithfriends.github.io/thanksgiving`) and share the link in the group chat. If you use a different address, change the two `biblewithfriends.github.io/thanksgiving` links near the top of `index.html` (og:url and og:image) or the link preview won't show the turkey.

If you edit `Code.gs` later, use **Deploy → Manage deployments → Edit → New version**. That keeps the same URL.

Until `API_URL` is set, the site runs in **preview mode**: it shows a copy of the sheet as of Nov 17 and sign-ups stay only on that screen.

## How it writes to the sheet
- **Serve** → puts the name in column D ("Sign up") of `2026-Service Sign Up`. If two people tap the same spot, the second person is asked to refresh or "Join". Joining adds `, Name` to the cell.
- **Dishes** → `2026-Dish Sign Up`, using the first empty row in that section (Table 1 = the sheet's "Room C" columns B/C, Table 2 = "Room D" columns F/G; beverages B/C, desserts F/G). If a section is full, a row is inserted above the blank row before the next section, so both tables stay lined up. There's no limit on how many dishes people can bring.
- **Invite** → adds a row to `2026 Invitation List` (Name, Shepherd, Notes, Sent, Response).
- **Day of** → everything on the Day of page (The evening and Before you leave home) lives on the `2026 Day Of Items` tab. The script creates it the first time and fills in the starter items. People can add, change, remove and drag items. The Order column holds the order on the page.

**Editing and moving:** Tapping any entry on the site lets people change it, move it or remove it. Dragging the ⠿ handle moves a serving name to another open spot, or a dish to another list. Before saving, the script checks that the cell still holds what the person saw. If someone changed it on the sheet in the meantime, nothing is overwritten and the person is asked to try again. "Church will provide" rows can only be changed on the sheet.

The tab names and the header words (Meat, Seafood, Carb, Other, Beverage, Desserts, "Task") are how the script finds things. Renaming a tab or header will break it. Adding or deleting rows is fine.

## Privacy
The site is public. The Invite page lists each friend's name, who invited them, and their answer. The **Notes** column is never sent to the site. To show only totals, set `SHOW_INVITE_NAMES = false` in `Code.gs`.

## Settings in index.html
`CONFIG` at the top holds the event date, time and place.
