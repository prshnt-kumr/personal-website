# Prashant Kumar — Personal Website

Single-page, zero-build static site. Hosted on Netlify. Maintained by an agent (see [`AGENT.md`](./AGENT.md)).

## Deploy in 60 seconds

**Easiest:** drag this whole folder onto <https://app.netlify.com/drop>.

**Better (continuous deploys):**
1. Push this folder to a new GitHub repo: `personal-website`.
2. In Netlify → *Add new site → Import from Git* → pick the repo.
3. Netlify reads `netlify.toml` automatically. No build command needed.
4. (Optional) set a custom domain in Netlify → *Domain settings*.

## File map

```
.
├── index.html          ← the whole site, single file
├── netlify.toml        ← Netlify build + security headers
├── _redirects          ← pretty-URL redirects
├── assets/
│   └── media/          ← drop .mp4 / .mp3 / .webm files here
├── AGENT.md            ← spec for the agent that maintains this site
└── README.md           ← you are here
```

## Editing content

The site is one HTML file. To update:

- **Headline / hero** — search for `class="hero"` in `index.html`.
- **AI / ML cards** — search for `<section id="ai"`.
- **Avarna section** — search for `<section id="avarna"`.
- **Book section** — search for `<section id="book"`.
- **Media gallery** — search for `<section id="media"`. Replace the three `placeholder` cards with `<video>` / `<audio>` elements pointing at files in `assets/media/`.
- **Journey / timeline** — search for `<section id="journey"`.
- **Contact** — search for `<section id="contact"`. Update the GitHub / LinkedIn / X URLs.

Or just ask Claude: *"update the website's hero to say X"* and it will edit the file.

## Adding media

1. Drop the file into `assets/media/` (e.g. `avarna-demo.mp4`).
2. Open `index.html`, find the matching placeholder card in the media section, and replace its `<div class="media-thumb">…</div>` with:

   ```html
   <video controls preload="metadata" poster="assets/media/avarna-demo-poster.jpg">
     <source src="assets/media/avarna-demo.mp4" type="video/mp4" />
   </video>
   ```

   For audio:

   ```html
   <audio controls preload="metadata" style="width:100%">
     <source src="assets/media/book-ch01.mp3" type="audio/mpeg" />
   </audio>
   ```

3. Commit & push. Netlify rebuilds in seconds.

## The agent

This site is intended to be a *living* page. An agent maintains it — see [`AGENT.md`](./AGENT.md) for the full spec and how to invoke it.
