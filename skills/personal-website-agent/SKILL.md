---
name: personal-website-agent
description: Use whenever Prashant asks to update, refresh, redesign, or extend his personal website (the folder "Personal Website"). Triggers include adding videos or media, publishing essays/insights, updating the book or Avarna sections, refreshing the hero, or running the weekly content refresh. Loads the agent spec, brand rules, and content conventions before any edit is made.
---

# Personal Website Maintenance Skill

## When to use this skill
Invoke any time the user (Prashant) refers to "the site", "the website", "my homepage", "the Avarna page", "the book section", or asks to:

- add a video, audio file, image, or any media
- publish or rotate an essay / insight / briefing
- add a journey / timeline entry
- update copy in any section
- run the weekly refresh
- redesign or restyle anything
- check for broken links or stale placeholders

## Before you do anything
Always read these three files in order, **before** any edit:

1. `AGENT.md` (project root) — full agent spec, brand rules, on-demand playbook, weekly job, quality bar.
2. `memory/feedback_site_style.md` — current visual style preferences (executive aesthetic, NOT dark/bold).
3. `memory/project_personal_website.md` — project context and stack.

## Workspace
- Project folder: `C:\Users\prshn\OneDrive\Documents\Claude\Projects\Personal Website`
- Main file: `index.html` (single file — every section lives in here).
- Media: `assets/media/`
- Deploy: Netlify (config in `netlify.toml`).

## Hard rules (full version in AGENT.md)
- **Stack is locked**: single HTML + CSS + minimal JS. No build tools. No frameworks.
- **Style is locked**: cream bg, navy primary, italic cornflower accent, serif headlines (Fraunces), Inter body.
- **Tone**: confident, restrained, no emoji, no exclamation marks in body copy.
- **Headlines** use Fraunces with an italic-accent phrase wrapped in `<span class="accent">…</span>` (or `class="it"` in the editorial layout).
- **Placeholders** are wrapped in `[Square Brackets]` so they are findable.
- **Never** revert to the dark/bold-portfolio aesthetic. Prashant pivoted away from that on 2026-05-21.
- **Product name is "Avarna"**, not "Avanta". Don't misspell it.
- **Prashant is not a "founder"** — Avarna is a working **POC**, no company formed. Acceptable framings: Builder · Building Avarna · Avarna (POC). Reject: Founder · CEO · startup · launched · Inc.
- **Book title** is *Machine Learning to Gen AI Agents: A Conceptual Journey from Foundations to Practice*.

## Standard tasks

### Add a video
1. Confirm the file is in `assets/media/` (or ask Prashant to drop it there).
2. Decide: featured slot (`#featured-video`) or thumbnail card (`.video-thumbs .vt`).
3. Replace the placeholder overlay/card with a `<video controls preload="metadata" poster="…">` element.
4. If no poster is provided, leave a `TODO` comment naming the expected poster path.

### Add an insight / essay
1. Open `index.html`, find `<section id="insights">`.
2. Insert a new `<article class="insight">` at the top of `.insights`.
3. If the grid now has more than 3 cards, comment out the oldest (don't delete).

### Add a journey entry
1. Find `<section id="journey">` → `.timeline`.
2. Insert a new `<div class="tl-item">` at the top with `tl-when`, `tl-what`, `tl-why`.

### Run the weekly refresh
Follow the playbook in `AGENT.md` §4 and reply with the `WEEKLY SITE REPORT` format.

## When in doubt
Ask Prashant before:
- Changing the visual style.
- Removing existing content (vs editing).
- Adding tracking, analytics, or external scripts.
- Auto-deploying.

## Done means
Verify `index.html` still has all expected sections (`#opener`, `#manifesto`, `#avarna`, `#book`, `#practice`, `#insights`, `#journey`, `#signoff`), no unclosed tags, no missing media references.
