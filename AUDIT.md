# UX audit — IB Diploma landing page

Date: 23 September 2026. Method: Nielsen Norman Group's 10 usability heuristics, plus a Lighthouse-style review of performance, accessibility, best practices and SEO, done by inspecting the code and assets. This is not an automated Lighthouse run. Run Lighthouse in Chrome DevTools on the deployed URL to get real scores.

## Fixed in this release

| Area | Issue | Fix |
|---|---|---|
| Performance | ~7 MB of photography shipped as PNG | Converted to WebP: hero 2.3 MB → 117 KB, study 2.7 MB → 118 KB, live classes 1.7 MB → 82 KB, athlete 365 → 38 KB |
| Performance | Hero image (LCP) competed with other requests | `fetchpriority="high"` on hero image, not lazy |
| Performance | Unused design-system JS bundle and 5 chained token stylesheets (render-blocking, values already inlined) | Removed from the deployable `index.html` |
| Accessibility (WCAG 2.2.2) | Looping video and logo carousel could not be paused | "Pause motion" control in the One of seven panel stops both |
| Accessibility (2.4.1) | No bypass block | "Skip to content" link, visible on keyboard focus |
| Accessibility (3.1.1) | Missing page language | `<html lang="en">` |
| Accessibility (2.5.8) | Footer links under 24px tall | Links padded to meet the minimum target size |
| SEO | No meta description or social preview | Meta description, Open Graph and Twitter card tags added |
| Heuristic 1 (visibility of status) | Two sports-count claims disagreed with the list | Flagged below, needs a content decision |

## Already passing

- Reduced motion respected throughout (`prefers-reduced-motion` stops all animation and the video).
- Every image has explicit width/height (no layout shift); below-the-fold images lazy-load.
- Single, consistent primary action ("Book a free admissions call") in the header, hero, mid-page and footer, plus a WhatsApp alternative (flexibility and efficiency of use).
- Timetable toggle exposes `aria-pressed`, the time readout is `aria-live`, and local time is computed from the visitor's time zone (match between system and the real world).
- FAQ uses native `<details>`, so it's keyboard and screen-reader accessible by default.
- Heading order is correct: one H1, section H2s, card H3s.
- Tap targets on buttons, toggles and FAQ rows are 44px or more.
- Text contrast meets 4.5:1 on all body copy (white on Deep Blue, Deep Blue on green/white).

## Search and paid-campaign readiness (added)

- Title, meta description, Open Graph, Twitter and robots tags now sit in the static `<head>`, so crawlers and link previews read them without running JavaScript.
- JSON-LD structured data: EducationalOrganization, Course (online IB Diploma) and an FAQPage built from the five on-page FAQs.
- A `<noscript>` copy of the page's key content (headline, proof points, timetables, FAQs, contact and CTA) for crawlers that don't run JavaScript. Googlebot and Google AdsBot do run JavaScript, so they also see the full rendered page.
- Hero image preloaded for a faster LCP, which feeds Google Ads landing-page experience.
- Google Tag Manager, using the same container as eastwood.global (GTM-PGWND4HR), so the existing Ads, GA4 and Meta tags fire here. Meta Pixel warns on non-production domains, which is expected.
- robots.txt allows crawling.

## Open items, needing decisions from Eastwood

1. **Live URL.** Set `<link rel="canonical">` in `index.html` and the Sitemap line in `robots.txt` once the domain is known.
2. **GTM triggers.** Confirm the container's conversion triggers include this page's enquiry-link clicks (`utm_content` = nav, hero, mid, footer).
3. **Sports count.** The copy says 15 disciplines, but the list shows 16. eastwood.global has the same mismatch.
4. **FAQ copy** needs sign-off from Shermine and Pooja. The FAQs on gosu, hps and webinar.eastwood.global couldn't be read and haven't been merged in.
5. **Recorded lessons.** The claim comes from a 2024 blog post. Confirm it still holds.
