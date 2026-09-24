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


## Tracking and consent

Everything the agency sent is implemented. No action needed before launch.

- **Google Tag Manager** GTM-PGWND4HR, same container as eastwood.global.
- **GA4** G-90VHGTGEM0. Loaded through GTM as on the main site; if GTM has not loaded it, the page loads it itself. Never counted twice.
- **Meta Pixel** 233289672835066. If the GTM container already runs this pixel, GTM keeps ownership of it and its events. If not, the page runs it. Never double-fired.
- **Meta events**, same as the main site:
  - `Contact` on WhatsApp and email clicks.
  - `EnquiryForm` on form submission, which fires on eastwood.global/enquire-now-form as today.
- **Google Ads**: the Ads specialist creates the conversion. GTM receives `enquire_click` and `contact_click` (`contact_method`) to trigger on if wanted.
- **Links**: no custom UTMs. Meta's dynamic parameters on the landing URL (fbclid, utm_*) are carried through to the enquire form.
- **Consent, opt-in regions only** (EEA, UK, Switzerland, detected by browser time zone):
  - Google Consent Mode v2 defaults to denied there, granted everywhere else. US traffic sees no banner.
  - The banner is the eastwood.global banner: same copy, same three choices (Manage Cookies, Decline All, Accept All), same leaf buttons.
  - Manage Cookies opens Essential (always on), Analytics (GA4) and Marketing (Google Ads, Meta). Choices map to Consent Mode and the Meta Pixel.
  - Choice is saved; "Cookie settings" in the footer reopens Manage Cookies.

### Launch check
1. Tag Assistant: GTM-PGWND4HR and G-90VHGTGEM0 each fire once.
2. Meta Pixel Helper: one PageView; one Contact per WhatsApp/email click.
3. EU connection: banner shows, tags held until Accept. Manage Cookies with Analytics only: GA4 fires, Meta does not. US connection: no banner.
4. Open with `?fbclid=test&utm_source=facebook`, click Enquire: both parameters arrive on the form URL.
