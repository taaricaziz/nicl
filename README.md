# NICL website redesign

A ground-up redesign of [nicl.com.pk](https://nicl.com.pk/), the website of
National Insurance Company Limited, the Government of Pakistan's insurer of
public property under Section 166(3) of the Insurance Ordinance, 2000.

This is a **static site with no build step**: eight HTML pages, one
stylesheet and one script. Serve the directory with any static file server
(`python3 -m http.server`, for instance). Links are extensionless (`/cover`,
`/claims`), which `vercel.json` maps to the `.html` files with `cleanUrls`;
on another host, enable the equivalent rewrite or add the extensions back.

Live at https://nicl-website.vercel.app, deployed from `main`.

## Pages

| File | Purpose |
| --- | --- |
| `index.html` | Home: mandate, schedule of cover, classes, claims steps, notices, offices |
| `cover.html` | The twelve classes of general insurance, each with perils and how to arrange it |
| `about.html` | Heritage (1976 → 2000 → 2001), mandate and functions, board, subsidiary, reports |
| `claims.html` | How to notify a loss, a per-class document checklist, survey and settlement, notice form |
| `contact.html` | Karachi head office, Lahore and Islamabad zonal offices, hours, enquiry form |
| `tenders.html` | Tender register under the Public Procurement Rules, 2004, with bidder grievance |
| `careers.html` | Vacancies and how selection works |
| `complaints.html` | Internal complaints, then the Ombudsman, SECP, SDRC and Insurance Tribunal |
| `404.html` | Not-found page, served by Vercel for unknown paths |
| `sitemap.xml`, `robots.txt` | Search-engine plumbing |

## Logo

The mark is a **proposed identity for the redesign, not NICL's official
logo**: a roundel in state green carrying an eight-point star in brass, the
same star that forms the lattice behind the home-page hero. It exists as:

- `assets/logo.svg`: horizontal lockup, emblem and wordmark, fixed colours
- `assets/logo-mark.svg`: emblem alone, for print and third parties
- `assets/favicon.svg`: emblem tuned for the tab
- `assets/og.png`: the 1200x630 social-preview card
- inline SVG in every page's header and footer, coloured from the theme
  tokens so it follows light and dark mode

To switch to the official logo, replace the four files above and the inline
`<svg>` inside the `.brand` links (identical in every page), then regenerate
`og.png`.

## Design

- **Palette**: lime-washed paper ground, deep state green (`#0f5a3a`), brass
  for seals and rules (`#a67c1f`). Light by default; dark follows the viewer's
  OS setting or the toggle in the top bar. Every colour is a token in
  `assets/site.css`.
- **Type**: Newsreader (display), IBM Plex Sans (body), IBM Plex Mono (policy
  codes, telephone numbers, labels), Noto Nastaliq Urdu for the Urdu lines.
  Loaded from Google Fonts with real fallback stacks.
- **Hero**: an eight-point star lattice drawn on a canvas in brass. The
  company has no product to photograph, only obligations it underwrites, so
  the backdrop is geometric rather than stock photography.
- **Accessibility**: skip link, landmarks, visible focus, `prefers-reduced-motion`
  honoured, keyboard-operable menu, labelled form controls, print stylesheet.
- **Performance**: no framework, no images, about 100 KB of HTML across all
  pages and one 20 KB stylesheet. Nothing blocks first paint except the fonts,
  which are `display=swap`.

## What is real and what is a placeholder

Facts on the site come from NICL's published pages and public records:
establishment in 1976, incorporation on 31 March 2000, paid-up capital of
Rs 2 billion, Ministry of Commerce oversight, Section 166(3), the 1994
subsidiary with Rs 448.20 million capital, Crop Loan Insurance from Rabi
2008-09, the classes of cover, the offices, UAN and telephone numbers, and
the CCP's 17.5% market-share figure.

Three things are deliberately marked as **examples** on the pages and must be
replaced with live data before launch:

- Tender listings (`tenders.html`) and the two tender lines on the home page.
- Career listings (`careers.html`) beyond the CEO vacancy, which was real.
- The three forms (claims notice, enquiry, complaint) are front-end only.
  They show a confirmation but send nothing; wiring them to a mailbox or
  ticketing system is a server-side step for NICL's IT team.

Service-level figures on the claims and complaints pages (acknowledgement in
three working days, surveyor within seven, written reply within fifteen) are
proposed standards, written so that NICL can commit to them or adjust them.
Board and management names are linked to the live site rather than copied,
because they change with each appointment.

## Editing

The pages share a header and footer. Change them in every file, or regenerate
the set with a small template script; the markup is plain enough that either
takes minutes.
