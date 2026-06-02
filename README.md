# Iberia '26 — trip site

A single-file, self-contained site (no build step). Interactive route map, day-by-day reference, and a "From the Road" journal feed with a photo lightbox. Designed to be edited by hand as the trip unfolds.

## Deploy (same as your finance PWA)
1. Put `index.html` at the root of a repo (e.g. `iberia-26`).
2. Repo → **Settings → Pages** → Source: `main` / root.
3. Live at `https://<you>.github.io/iberia-26/`. Share that link with Ira & friends.

## Two content models, by design
- **`TRIP.stops[]`** — the *stable reference*. Drives the route map + day-by-day cards. You set this once.
- **`TRIP.journal[]`** — the *live feed*. Newest entries show first; this is where photos + notes go as you travel.

Both live in the `TRIP` object near the bottom of `index.html`, marked **"EDIT YOUR TRIP HERE."**

## Adding a journal entry
```js
{ date:"2026-09-12", stop:"Biarritz", title:"First surf",
  body:"Côte des Basques at low tide, glassy…",
  photos:[
    {src:"img/biarritz-1.jpg", caption:"Dawn paddle-out"},
    {src:"img/biarritz-2.jpg", caption:""}
  ] }
```
- Drop photos in an `/img` folder and reference them, or paste links from a host.
- `stop` should match a stop name — that stop's card then shows a **"📷 N from the road →"** link.
- The gallery has a built-in **tap-to-enlarge lightbox** (arrow keys / swipe through, Esc to close). A sample entry is included — delete it once you add your own.

## The Bars & Eats map
Embeds your Google My Map via `TRIP.googleMapId`. For friends to see it: open the map in Google → **Share** → **"Anyone with the link."** Edit pins in Google as normal; the site reflects them automatically.

## Later: live phone uploads (optional)
The journal reads from the `journal[]` array today. When you want to post from your phone mid-trip without pushing to git, we swap that one data source to **Firebase** (Storage + Realtime DB) with a PIN-gated "+ New entry" form — the same public-read / PIN-to-write pattern as your finance tracker. The display never changes; only where entries come from.

## Design notes
- Type: DM Serif Display + Hanken Grotesk. Palette in the `:root` CSS variables (clay / sea / paper).
- Map: Leaflet + CARTO Positron tiles (free, attributed).
