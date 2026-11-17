# Thanksgiving Love Feast 2026 — planning site

A site for the church family with five pages (Layout, Invite, Day of, Serve, Dishes): the room map, the invitation list, a day-of checklist, open serving spots, and dishes for Space C and Space D. Everything reads from and writes to the **Thanksgiving Dinner Service Sign Up** Google Sheet.

## Files
- `index.html` — the whole website (put it on GitHub Pages)
- `Code.gs` — the Google Apps Script that connects the site to the sheet

## Set up (about 10 minutes)
1. Open the Google Sheet → **Extensions → Apps Script**. Paste `Code.gs` and save.
2. Click **Run → testRead** once and approve the permissions. Check **View → Logs**; you should see the slots and dishes.
3. **Deploy → New deployment → Web app**. Set Execute as **Me** and Who has access **Anyone**. Copy the URL that ends in `/exec`.
4. In `index.html`, paste that URL into `API_URL: ""` near the top.
5. Upload `index.html` to a GitHub Pages repo (for example `biblewithfriends.github.io/thanksgiving`) and share the link in the group chat.

If you edit `Code.gs` later, use **Deploy → Manage deployments → Edit → New version**. That keeps the same URL.

Until `API_URL` is set, the site runs in **preview mode**: it shows a copy of the sheet as of Nov 17 and sign-ups stay only on that screen.

## How it writes to the sheet
- **Serve** → puts the name in column D ("Sign up") of `2026-Service Sign Up`. If two people tap the same spot, the second person is asked to refresh or "Join". Joining adds `, Name` to the cell.
- **Dishes** → `2026-Dish Sign Up`, using the first empty row in that section (Room C = columns B/C, Room D = F/G; beverages B/C, desserts F/G). If a section is full, a row is inserted above the blank row before the next section, so Room C and Room D stay lined up.
- **Invite** → adds a row to `2026 Invitation List` (Name, Shepherd, Notes, Sent, Response).
- **Day of** → items people add to The evening, Before you leave home, or Supply boxes go on a new tab, `2026 Day Of Items`. The script creates this tab the first time. To remove an item, delete its row there.

The tab names and the header words (Meat, Seafood, Carb, Other, Beverage, Desserts, "Task") are how the script finds things. Renaming a tab or header will break it. Adding or deleting rows is fine.

## Privacy
The site is public. The Invite page lists each friend's name, who invited them, and their answer. The **Notes** column is never sent to the site. To show only totals, set `SHOW_INVITE_NAMES = false` in `Code.gs`.

## Settings in index.html
`CONFIG` at the top holds the event date, time and place, plus `TARGETS`, the number of dishes hoped for per category per room (now meat 8, seafood 3, carbs 5, sides 5, desserts 8, drinks 3). Change them freely.
