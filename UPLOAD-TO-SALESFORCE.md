# Uploading howdy-event-hub.css to Salesforce

Blackthorn requires the CSS to be served as a **public file with MIME type `text/css`**. The most reliable way is a Static Resource exposed via a Site, or a public Files/Content asset. Below are the two paths — pick the one that fits how your org is set up.

---

## Option A — Static Resource via a Salesforce Site (recommended)

This gives you a stable, public, no-auth URL with the right MIME type.

1. **Upload as a Static Resource**
   - Setup → quick-find **Static Resources** → **New**
   - Name: `howdy_event_hub_css`
   - Cache Control: **Public**
   - File: select `howdy-event-hub.css`
   - Save

2. **Expose via a Site (if your org doesn't already have one)**
   - Setup → quick-find **Sites** → **New** (Salesforce Sites, not Experience Cloud)
   - Default Web Address: e.g. `howdy-events` → site URL becomes something like `https://howdy-developer-edition.na123.force.com/howdy-events`
   - Active: ✓
   - Save
   - In the Site detail, click **Public Access Settings** → enable **Read** on the Static Resource

3. **Get the public URL**
   - The CSS will be reachable at:
     `https://<your-site-domain>/resource/howdy_event_hub_css`
   - Open it in an incognito browser tab to confirm:
     - It returns the CSS contents
     - Response header `Content-Type: text/css` (check DevTools → Network)

4. **Paste into Blackthorn**
   - Navigate to the **Event Group** record (the Howdy.com Events group)
   - Edit the **Custom CSS Url** field → paste the URL from step 3
   - Save
   - Reload `https://events.blackthorn.io/en/.../g/Ht8NW0cfKm` — styling applies.

---

## Option B — Salesforce Files (quick, no Site required)

Works if you can publish a File as a public link. The Content-Type header is generally correct for `.css`, but **verify it** before trusting it.

1. App Launcher → **Files** → **Upload Files** → choose `howdy-event-hub.css`
2. Open the file → **Public Link** → **Create**
3. Open the public link in incognito → confirm `Content-Type: text/css` in DevTools Network
4. Paste the link into the Event Group's **Custom CSS Url** field.

If the Content-Type comes back as `application/octet-stream` or anything other than `text/css`, browsers may refuse to load it as a stylesheet — fall back to Option A.

---

## Hierarchy reminder

Blackthorn applies Custom CSS at three levels (most specific wins):

1. **Event** — overrides everything else, for one event only
2. **Event Group** ← *this is where you're putting the file*
3. **Event Settings** — broadest default

You only need this URL pasted on the Event Group record.

---

## After uploading

- Reload the hub page in a real browser (not just Blackthorn's preview), hard refresh with **Cmd+Shift+R** to bypass any CSS cache.
- If the layout still shows the old thumbnail grid, open DevTools → Network and confirm `howdy-event-hub.css` is loading with status 200 and the right MIME type.
- If you ever want to tweak the styling, edit `howdy-event-hub.css` locally and re-upload (replace the Static Resource file or re-upload the File and re-publish the link — same URL).

---

## Quick-tweak cheatsheet

Most visual changes only need a single CSS variable in `:root`:

| Want to change… | Edit this variable |
| --- | --- |
| Accent / CTA color | `--howdy-accent` (and `--howdy-accent-fg` for text on it) |
| Background | `--howdy-bg` |
| Body text color | `--howdy-fg` / `--howdy-muted` / `--howdy-subtle` |
| Card border | `--howdy-border` |
| Card corner radius | `--howdy-radius-md` |
| Vertical spacing between events | `--howdy-row-gap` |
| Font family | `--howdy-font` |

To change the "Register" CTA label, find `a.grid-item::after` and edit the `content:` line.
