# Norwich Builders

Website for **Norwich Builders**, a building firm covering Norwich and the
surrounding areas of Norfolk. Kitchens, bathrooms, extensions, renovations
and conversions.

Live site: https://www.norwichbuilders.co.uk/

## What this is

A static site — plain HTML, one shared stylesheet, and a small amount of
vanilla JavaScript. No build step, no framework, no package manager. Open
`index.html` in a browser and it works.

## Running it locally

Any static file server will do. From the project root:

```
python3 -m http.server 8080
```

Then visit http://localhost:8080/. A server is needed rather than opening
the files directly, because the header and footer are fetched at runtime.

## Layout

```
index.html              Homepage — hero, five services, closing call to action
pages/
  about.html            About the business
  services.html         Services index
  services/             One page per service (kitchens, bathrooms,
                        extensions, renovations, conversions)
  gallery.html          Project photos, filterable, masonry layout
  contact.html          Enquiry form, contact details, service-area map
  thank-you.html        Post-enquiry confirmation
  privacy-policy.html
components/
  header.html           Shared header, injected at runtime
  footer.html           Shared footer, injected at runtime
assets/
  imgs/                 Client project photos and generated site images
  Font/timeless/        Display typeface
global.js               Injects the header and footer, mobile nav
style.css               All shared styling
```

`components/header.html` and `components/footer.html` are fetched by
`global.js` into `#header-placeholder` and `#footer-placeholder`. Edit
them once and every page picks the change up.

## Enquiry form

The contact form posts to [Web3Forms](https://web3forms.com), which
forwards submissions to the business inbox. It needs an access key before
it will send:

1. Request a key at web3forms.com for `norwichbuilders@hotmail.com`.
2. Replace `REPLACE_WITH_WEB3FORMS_ACCESS_KEY` in `pages/contact.html`.

Until that is set the form refuses to submit and shows the phone number
and email address instead, rather than silently dropping an enquiry. The
key is a public identifier and is safe in client-side source.

## Images

Project photos are the client's own. Site images (hero, service cards, service
pages and the gallery) are all generated from `assets/imgs/gallery/`, resized
to a max width of 1600px with EXIF/GPS metadata stripped. The raw source set
is `assets/imgs/drive-download-20260917T195930Z-1-001/` (excluded from
deployment via `.vercelignore` since the originals still carry metadata; not
excluded from git).

The gallery uses a CSS-grid so photos display in fixed-height tiles, cropped
to a consistent shape.

## Brand

| | |
|---|---|
| Navy | `#2c3172` — dominant |
| Navy deep | `#1f2352` — large fills, hover states |
| Gold | `#e5a824` — accent only: buttons, links, small highlights |
| Headings | Timeless Bold |
| Body | DM Sans |

Gold is never used for large fills or section backgrounds.

## House rules

- **No motion.** No keyframes, no scroll-triggered reveals, no carousels,
  marquees, parallax, animated counters or autoplay video. Colour and
  opacity transitions on hover are fine. This is the client's most
  specific request — check any new component against it.
- **Never invent a business fact.** Certifications, insurance, licences,
  years trading, staff numbers, job counts, ratings and testimonials are
  all unconfirmed. Leave a visible `TODO` rather than filling a gap.
- No `aggregateRating` or `review` structured data.
- Alt text describes what a photo actually shows.

## Deployment

Deploys as static files. `vercel.json` carries the security headers,
including a content security policy that allowlists the Web3Forms
endpoint, Google Fonts and the Leaflet CDN used by the contact map.
`serve.json` mirrors it for local previews.

---

Built by [Ontek Systems](https://onteksystems.com).
