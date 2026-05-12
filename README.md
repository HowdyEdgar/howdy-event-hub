# Howdy.com Event Hub — Blackthorn Custom CSS

Custom stylesheet that converts the Blackthorn Aspen event group listing into a clean text list with pill CTAs, matching the [howdy.com](https://www.howdy.com/) brand (Inter typography, black pill buttons, minimal palette).

## Live URL for Blackthorn

Paste this into the **Custom CSS Url** field on the Event Group record in Salesforce:

```
https://cdn.jsdelivr.net/gh/HowdyEdgar/howdy-event-hub@main/howdy-event-hub.css
```

jsDelivr serves the file with `Content-Type: text/css` and caches at the CDN edge. Edits pushed to `main` propagate in ~10 seconds. If a change doesn't show up, append `?v=2` (or any number) to bust the cache.

## Editing

1. Edit `howdy-event-hub.css` locally or directly in the GitHub web UI.
2. Commit and push to `main`.
3. Reload the Blackthorn hub page (hard refresh with Cmd+Shift+R).

## What it does

- Converts the multi-column Aspen grid into a vertical list of event rows.
- Hides event banner thumbnails (text-only rows).
- Adds a black pill "Register" CTA on each row.
- Restyles the search bar, sidebar filters, and "Load more" button to match Howdy's pill aesthetic.
- Hides the language selector.
- Mobile-responsive (single-column stack with full-width CTA below ~640px).

## Quick tweaks

Most visual changes can be made by editing the CSS custom properties at the top of `howdy-event-hub.css`:

| To change... | Edit the variable |
| --- | --- |
| Accent / CTA color | `--howdy-accent` (and `--howdy-accent-fg`) |
| Background | `--howdy-bg` |
| Text color | `--howdy-fg` / `--howdy-muted` / `--howdy-subtle` |
| Card border | `--howdy-border` |
| Card corner radius | `--howdy-radius-md` |
| Gap between rows | `--howdy-row-gap` |
| Font family | `--howdy-font` |

The "Register" button label is hard-coded in `a.grid-item::after { content: 'Register' }` — search for that line to change the wording.
