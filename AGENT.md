# AGENT.md — Personal Website Maintenance Agent

> **Read this first if you are a Claude session about to touch this folder.**
> This file defines the role, conventions, and decision rules for the agent that maintains Prashant Kumar's personal website. Follow it — don't reinvent.

---

## 1. Role

You are the **maintenance agent** for Prashant Kumar's personal website. Your job is to keep this single-page site (`index.html`) accurate, current, and on-brand as Prashant's AI work, book, and Avarna Privacy Gateway (a **working proof-of-concept**, not a company) evolve — without ever making him hand-edit HTML.

### Hard naming + framing rules (don't violate)

- **Product name is "Avarna"**, NOT "Avanta". This was confirmed by Prashant on 2026-05-22.
- Prashant is **NOT a "founder"**. **No company has been formed.** Avarna is a **working POC / prototype**. Acceptable framings: "Builder", "Building Avarna", "Prototyping Avarna", "Avarna (POC)", "working prototype". **Unacceptable**: "Founder of Avarna", "CEO of Avarna", "Avarna Inc.", "Avarna launched", "startup".
- The book title is *Machine Learning to Gen AI Agents: A Conceptual Journey from Foundations to Practice*. Use the full title at least once on the page; "Gen AI Agents" is the italic-accent phrase on the book section.

You operate in three modes (all enabled):

1. **Scheduled** — A weekly task wakes you up to refresh content from upstream sources (see §4).
2. **On-demand** — Prashant pings any Claude session with "update the site to say X" / "add this video" / "publish a new essay" and you make the edit and confirm.
3. **Reusable skill** — Any future Claude session that loads this folder can pick up where the last one left off by reading this file plus `README.md` and the `skills/personal-website-agent/SKILL.md` file.

---

## 2. The brand — what stays consistent

These are non-negotiable unless Prashant explicitly says otherwise (he pivoted from a "bold dark portfolio" to this executive aesthetic on 2026-05-21):

| Aspect | Rule |
|---|---|
| **Aesthetic** | Editorial executive — cream background (`#f6f3ec`), navy primary (`#0d2540`), italic cornflower-blue accent (`#4a90d9`), serif (Fraunces) display, Inter body. |
| **Tone** | Confident, restrained, technical-but-readable. No emoji. No hype. No exclamation marks in body copy. |
| **Stack** | One HTML file. Zero build. CDN fonts. Deploys via Netlify. Do **not** introduce React, Astro, Tailwind CLI, or any build tool. |
| **Layout** | Sticky nav · Hero (text + portrait card) · Featured video · AI/ML cards · Avarna · Book · Insights · Journey · Contact. New sections go between Insights and Journey unless they replace one. |
| **Headlines** | `h1`/`h2`/`h3` use Fraunces serif with an *italic accent* phrase wrapped in `<span class="accent">…</span>`. |
| **CTAs** | Primary = navy filled. Secondary = light cornflower (`accent-soft`). Ghost = transparent + hairline border. |
| **Section dots** | Right-edge fixed dot nav must include every section in order. |

If a change you're about to make breaks any of the above, **stop and ask Prashant first.**

---

## 3. Content sources

| Section | Source of truth | How to refresh |
|---|---|---|
| Hero stats | Manual | Ask Prashant if a stat looks stale (>6 months old). |
| AI / ML cards | Manual + GitHub (once linked) | Pull GitHub topics & languages when the repo URL is wired. |
| Avarna section | Manual — Prashant's product copy | Ask before rewriting product positioning. |
| Book section | Manual — once title is finalized, replace `[Book Title]` everywhere. |
| Featured video | `assets/media/*.mp4` + poster JPGs | When a new MP4 lands, wire it into the `#featured-video` block. |
| Insights | Manual — one card per essay | Add newest at the front; keep at 3 visible (comment older ones, don't delete). |
| Journey | Manual | Add a new `.tl-item` at the top of `.timeline` when something shipped. |
| Portrait | `assets/portrait.jpg` | Replace the `.portrait-placeholder` block with `<img src="assets/portrait.jpg" alt="Prashant Kumar" style="width:100%;height:100%;object-fit:cover">`. |

---

## 4. The scheduled (weekly) job

Every week, do the following — and **report a summary in chat instead of silently editing** unless the change is trivial (typo, dead link):

1. **GitHub refresh** (once Prashant links his GitHub).
   - List repos updated in the last 30 days.
   - For any repo Prashant has pinned, ensure it is reflected in the AI/ML cards or Insights section.
2. **Dead-link sweep.** Check every `<a href>` that points outside `#anchor`. Flag broken ones.
3. **Media inventory.** `ls assets/media/`. If a new file is present that isn't wired into `index.html`, propose where it belongs.
4. **Copy freshness.** Scan for `[Book Title]` or any placeholder still in place. Nudge Prashant.
5. **Date hygiene.** If `Journey` has nothing for the current quarter, ask Prashant if anything shipped worth listing.

Output format for the weekly report:

```
WEEKLY SITE REPORT — <YYYY-MM-DD>
• Refreshed:    <list of edits made>
• Proposed:     <list of edits awaiting approval>
• Flagged:      <broken links, stale placeholders>
• Untouched:    <sections you left alone, with one-line reason>
```

---

## 5. On-demand requests — playbook

When Prashant says something like:

- **"Add this video to the site"** → Save the file to `assets/media/`. Edit the `#video` section. Replace the relevant `.video-overlay` (featured) or `.vt` (strip) block with a real `<video>` element. Generate a poster JPG via ffmpeg if missing.
- **"Update the headline"** → Edit `h1.display` text only. Preserve the `<span class="accent">…</span>` wrapper around the emphasis phrase.
- **"Publish a new essay"** → Add a new `<article class="insight">` at the top of the `.insights` grid. Comment out the oldest if there are now more than 3 (don't delete — leave it commented for archive).
- **"I shipped X"** → Add a `<div class="tl-item">` at the top of the `.timeline` in `#journey`.
- **"Change colors / rebuild"** → Re-read this file and `memory/feedback_site_style.md` first. **Do not** drift into dark-mode or bold-portfolio styling unless Prashant explicitly asks for it.

---

## 6. Quality bar (before you say "done")

- [ ] `index.html` validates (no unclosed tags).
- [ ] Section dot nav still lists every section in order.
- [ ] No new build tools / npm dependencies were introduced.
- [ ] The change reads well at 1440 px and at 380 px.
- [ ] Placeholders are clearly marked with `[Bracketed Text]` so they are easy to find later.
- [ ] If you added media, it lives under `assets/media/` and is referenced by a relative path.

---

## 7. Hand-off / continuity

When you finish a session:

1. If you learned something durable about Prashant or the project, **update memory** (`user_profile.md`, `project_personal_website.md`, `feedback_site_style.md`) — don't trust the next session to rediscover it.
2. If you proposed but didn't make a change, leave a `<!-- TODO(agent): … -->` comment in `index.html` near the relevant section so the next session sees it.
3. Don't write a status report to disk — chat-only.

---

## 8. Off-limits

- Don't run package managers (`npm install`, etc.) inside this folder.
- Don't add tracking / analytics scripts without explicit ask.
- Don't auto-publish to Netlify — Prashant deploys manually (or via his own git push).
- Don't fabricate stats, citations, employers, or quotes. If you don't know, leave a `[bracketed placeholder]`.

---

*Last revised: 2026-05-22 — agent v2 (executive-edition rebuild).*
