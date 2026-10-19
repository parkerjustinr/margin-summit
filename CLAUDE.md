# Working in this repo

One-page event site. Plain HTML, CSS, vanilla JS. No framework, no build step. Deploys to GitHub Pages from `main`, root.

## Where things live
- `data/event.json` - all content. Change copy here, not in the markup.
  - `sections` sets order and on/off for every section. Nav and footer follow it.
  - `tracks` drive the agenda columns (track-1, track-2, track-3 in CSS, in the order listed). Tracks are told apart by column, number and weight, not color.
  - Schedule sessions carry `tiers`, which the ticket matrix and calendar downloads use.
  - Session `speakers` are ids of featured speakers (one talk each, plus at most a panel). Everyone else goes in `guests` as name and company only.
  - Ticket rows with `from` (`day:<id>`, `track:<id>`, `session:<id>`) build their preview from the schedule. Rows without `from` show `detail`.
- `styles.css` - design tokens at the top of `:root`. Archivo for all text, IBM Plex Mono for times, dates and numbers only. Change tokens first, then section styles.
- `app.js` - one renderer per section in the `R` object. To add a section: add a renderer `R.<id>`, then add `{ "id": "<id>", "label": "...", "on": true }` to `sections`.
- `#hero-moment` in `index.html` is reserved for the one big hero element. It holds the seat map: 600 seats in three track blocks of 200 (`renderSeats` in `app.js`). Visitors claim one seat; it shows on the confirmation and in the .ics, or one is assigned at random on submit.

## Built-in features (keep them working)
- Featured speaker plus grid. Speakers link to their sessions and sessions link back, switching the day tab if needed.
- Schedule day tabs (arrow keys work), tracks as side-by-side columns on desktop, "show my time" toggle (Intl API), per-day .ics download.
- Ticket breakdown matrix: pick a column to choose a ticket, hover or focus a row for a side preview on desktop, tap a row to open it inline on phones. No sideways scroll on phones. Cost-per-day row is computed.
- Demo registration with validation and a confirmation state. Nothing is sent anywhere.
- Skip link, visible focus, reduced-motion support.

## Rules
- No em dashes anywhere, in code comments or copy. Use a hyphen.
- Left-align text. No eyebrow labels over headings. No decorative numbering. No gradients. No drop shadows at rest.
- Every color means one thing (a track, a state, the selected ticket). Keep at least one big field of color per screen.
- Check 360, 390, 768 and 1280 px wide: no sideways scroll, no clipped headings.
- Commit and push after every finished change.
