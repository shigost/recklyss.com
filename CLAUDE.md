# Recklyss Studios website (recklyss.com)

Project guide for Claude Code. Read this before making changes.

## What this is

The new home of **Recklyss Studios**, Alyssa Stills’ independent creative studio (an Arizona LLC). The site showcases her games, the character **Shigost**, digital art, and interactive experiences. It replaces an old site built on Universe (univer.se), which shuts down December 31, 2026.

The site’s one job is **the studio’s creative work**. Client services belong to Studio Stills (a separate site) and Alyssa’s personal career story belongs on her portfolio, so neither goes here.

## Hosting and deployment

- Repo: `shigost/recklyss.com`, branch `main`, served by GitHub Pages from the root folder.
- Current live URL: `https://shigost.github.io/recklyss.com/`
- Pushing to `main` deploys automatically. Always commit with a short, clear message.
- **Do not add a `CNAME` file or custom domain yet.** The recklyss.com domain is being transferred to Dynadot. Alyssa will say when it’s time.
- `play.recklyss.com` points to `shigost.github.io` and serves Vibe Booth from a different repo. Never do anything that could break it.

## Files

- `index.html` is the whole site in one self-contained file (HTML, CSS, and JavaScript inline). No build step, no frameworks.
- Old code from the Universe site is archived on Alyssa’s computer, **not** in this repo, because the repo is public. Don’t add archive files here.

## The vision

A scroll-driven, clickable journey through a 2.5D world. As visitors scroll, the camera follows Shigost through eight chapters:

1. **Outer space** (built): hero billboard advertising Vibe Booth sits on an asteroid. Scrolling zooms out, Shigost jumps off and parachutes down.
2. **Grassy hills** (built): she lands, then walks right toward the jungle.
3. **Jungle** (built): she hops into a misty jungle and rests by the vine harp.
4. Sand dunes (next)
5. Beach
6. Reef
7. Deep ocean
8. The island

When scrolling stops, each chapter plays an idle loop. Objects in each scene act as doors to other content (games, art, and so on). Build chapters one at a time, and keep earlier chapters working.

## Art direction

- Alyssa’s cartoon style blends **Studio Ghibli, Dr. Seuss, and Adventure Time**: soft painterly skies and haze, curly whimsical shapes, and confident dark outlines on foreground objects.
- Everything currently drawn is **placeholder art** made from SVG. Alyssa will draw the real art in layers, which will replace the placeholders piece by piece. Keep each visual element a separate layer so it can be swapped easily.
- Avoid anything that looks cheesy or clip-art: no bubbly fonts, no “Click me!” speech bubbles, no flat candy colors. Clickable things are marked with a soft dashed halo plus a small hint at the bottom of the screen.
- Font: Bricolage Grotesque (Google Fonts), often condensed.
- Shigost is referred to as **she**.

## Characters and interactions

- **Shigost**: small white ghost with big dark eyes. In space she has a portal gun; tapping her fires it and opens a portal teasing the Space Explorer game.
- **Moon snail** on the asteroid hides in its shell when tapped. A **star whale** drifts in the background.
- **The painter** in the hills: a lanky, feathered lavender creature (inspired by Alyssa’s own character studies). Tapping opens the future art gallery.
- **Puffsheep** in the hills bounce when tapped.
- **Lemur** in the jungle hangs by its tail and waves when tapped. A **parrot** sits on a branch.
- **Vine harp** in the jungle: dragging across the vines plays notes (Web Audio, works with touch).

## Games and links

| Game | Status | Link |
| --- | --- | --- |
| Vibe Booth | Playable now (the star of the hero) | https://play.recklyss.com |
| Dedog | Playable prototype (Figma Make) | https://dedog.figma.site |
| Pathogen | Playable prototype (Figma Make), description still needed from Alyssa | https://pathogen.figma.site |
| Shigost Space Explorer | Buggy prototype, **not linked yet**; still shown as a concept | https://space.figma.site |
| Shigost (the big game) | In production | none yet |

Space Explorer’s planets from an older prototype were named Elystra, Vulcron, Orryx, Nymia, and Xérah.

## How the code is organized (inside `index.html`)

- `place(html, x, y, w, h, options)` puts an object into the world at world coordinates. Options: `k` (parallax), `kx` and `ky` (separate parallax per axis), `z` (layer), `cls`, and `id`.
- `shigostAt(p)` returns Shigost’s position and state for scroll progress `p` (0 to 1). The constant `S` (currently 0.70) marks where space and hills end and the jungle portion begins.
- `camAt(p, vw, vh)` returns the camera position and zoom as a list of keyframes.
- `CHAPTERS` defines chapter names, scroll ranges, and rest points (used for the reduced motion version).
- World landmarks: asteroid near y 0, hills ground `GROUND` at y 15800, jungle floor `JG` at y 15900, jungle spans x 4250 to 12500. New chapters continue to the right of the jungle.
- To add a chapter: extend the scroll length (`#journey` height), add Shigost and camera keyframes after the jungle, add a `CHAPTERS` entry, mark its dot as built in `#rail`, and add its scene objects.

## Must keep working

- Regular navigation and the Games, About, and Join sections below the journey, so nobody has to scroll the whole world to find the Play button.
- The reduced motion version (`prefers-reduced-motion`), which jumps between chapter rest points.
- Mobile: test at about 390 by 844 as well as desktop. Touch must work for everything clickable.
- Light and dark mode for the content sections.

## Open to-dos

- Write a real description and card art for **Pathogen** once Alyssa explains the game.
- Connect the **Join** form to a real mailing list (Formspree or similar) with spam protection. The old subscriber list is full of bot signups and must be cleaned before importing.
- Fix and eventually link **Space Explorer** through Shigost’s portal.
- Build the **sand dunes** chapter next.
- After the domain transfer: point recklyss.com at GitHub Pages and set up email forwarding for info@recklyss.com.
- About section copy is a draft.

## Working with Alyssa

- She’s a designer who ships and likes clear, step-by-step guidance for anything technical.
- In replies, use Oxford commas and never use em dashes.
- Avoid promising dates on the site. Use statuses like “in production” or “coming soon” instead.
