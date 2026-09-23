# Eastwood Global — IB Diploma landing page

Static landing page for the online IB Diploma Programme. There's no build step.

## Structure

```
index.html      Page (markup, inline styles, behaviour)
support.js      Runtime that renders index.html. Keep it next to index.html
assets/         Images (WebP/PNG), logo lineup, background video
AUDIT.md        NN/g + Lighthouse-style audit, fixes and open items
```

## Run locally

Serve the folder over HTTP. Opening the file directly won't work, because the runtime fetches the page:

```
npx serve .
# or
python3 -m http.server 8080
```

## Deploy

Any static host works: GitHub Pages, Netlify, Vercel or S3. For GitHub Pages, push to `main` and set Pages → Source → `main` / root.

## Editing

- Copy lives in `index.html`. Search for the visible text.
- Timetable cities, time zones and coordinates are in the `CITIES` array. Pins are projected onto `assets/eg-map-world.webp`. If you swap the map, the `projX` / `projY` constants need re-calibrating.
- Sessions are set in `SESS`, in minutes from midnight Swiss time (`am: 8:00–13:30`, `pm: 15:00–20:30`).
- Enquiry links use `https://www.eastwood.global/enquire-now-form` with `utm_source=ib&utm_medium=landing&utm_content=<position>`.

## Before launch

Review the open items in `AUDIT.md`, then run Lighthouse on the deployed URL.
