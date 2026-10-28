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

## Who Shigost is

- Shigost is a **gost**, never a “ghost,” anywhere: copy, alt text, labels, comments, code, and this file. Definition, to use where it fits: “Shigost is a gost: a spirit who has crossed into a realm beyond, neither quite alive nor quite gone.”
- **Her real design** (placeholders must match it): a long, oversized white hoodie that reaches about her knees, hood up. Her white face sits inside a teardrop-shaped opening in the hood that points downward, with two big, round, glossy black eyes. Drawstrings hang from the neck, long sleeves mostly cover small hands, and she wears chunky white high-top sneakers. She is **not** a sheet ghost: no wavy hem.
- **Never put her on a yellow or gold background, and never near anything that resembles the Snapchat logo.** This covers card art, the billboard, the About art, and the world (the hills sun is a rose haze and the jungle light is mint for this reason). Gold is fine for buttons and small accents away from her.
- She loves music, especially EDM, and wants to play it everywhere she explores.

## The game and Vibe Booth

- **Shigost** (the big game, in production) is a 3D explorer platformer and collectathon in the spirit of Banjo-Kazooie and Yooka-Laylee, with music at its heart. The DJ gameplay teaches real DJ skills. She travels to new environments, meets peoples and creatures, deals with changing weather, helps locals who then become her crowd and cheer at her shows, cleans up polluted places, and collects orbs, totems, notes, and sounds to build her gear and play her sets. There are environmental puzzles, character interactions, and boss fights.
- **Vibe Booth** (play.recklyss.com) is the playable teaser for the music side of the game: Shigost on her first tiny island. It will get a new name later and become an island in the full game.
- **The game’s other islands are private and not live.** Describe the kinds of worlds in general terms only. Never name, show, or link an individual island.

## Characters and interactions

- **Shigost**: see “Who Shigost is” above. In space she has a portal gun; tapping her fires it, the camera eases out, and a portal opens teasing the Space Explorer game. Her poses are separate arm layers (arms down, arms up for jump, fall, and parachute with the lines in her hands, and the gun arm), sneakers that step while walking, and idle loops per chapter. The small reusable version (`#gostSym`) is built from the same parts for cards, About, and the billboard DJ.
- **Moon snail** on the asteroid hides in its shell when tapped. A **star whale** drifts in the background.
- **The painter** in the hills: a lanky, feathered lavender creature (inspired by Alyssa’s own character studies). Tapping opens the future art gallery.
- **Puffsheep** in the hills bounce when tapped.
- **Lemur** in the jungle hangs by its tail and waves when tapped. A **parrot** sits on a branch.
- **Vine harp** in the jungle: dragging across the vines plays notes (Web Audio, works with touch).

## Games and links

| Game | Status | Link |
| --- | --- | --- |
| Vibe Booth | Playable teaser (the star of the hero) | https://play.recklyss.com |
| Dedog | Playable prototype (Figma Make) | https://dedog.figma.site |
| Pathogen | Playable prototype (Figma Make), description still needed from Alyssa | https://pathogen.figma.site |
| Shigost Space Explorer | Buggy prototype, **not linked yet**; still shown as a concept | https://space.figma.site |
| Shigost (the big game) | In production | none yet |

Space Explorer’s planets from an older prototype were named Elystra, Vulcron, Orryx, Nymia, and Xérah.

## How the code is organized (inside `index.html`)

- `place(html, x, y, w, h, options)` puts an object into the world at world coordinates. Options: `k` (parallax), `kx` and `ky` (separate parallax per axis), `z` (layer), `cls`, `id`, and `keep` (never culled). It adds the object to the current chapter group, set with `chapterGroup(name)`.
- `hit(x, y, w, h, fn)` adds an invisible tap area; `halo(x, y, d, chapter)` adds the dashed halo.
- `shigostAt(p)` returns Shigost’s position and state for scroll progress `p` (0 to 1). The constant `S` (currently 0.70) marks where space and hills end and the jungle portion begins.
- `relayout(vw, vh)` builds the camera keyframes for the current viewport; `camAt(p)` reads them. Each keyframe names a world box that must stay in view, and `fit()` chooses zoom and center inside the safe frame (below the header, above the HUD, inside the safe areas). It also picks the hero layout: copy inside the billboard (wide), call to action below it (`stack`), or beside it (`side`).
- `CHAPTERS` defines chapter names, scroll ranges, and rest points (used for the reduced motion version).
- World landmarks: asteroid near y 0, hills ground `GROUND` at y 15800, jungle floor `JG` at y 15900, jungle spans x 4250 to 12500. New chapters continue to the right of the jungle.
- To add a chapter: extend the scroll length (`#journey` height), add Shigost and camera keyframes after the jungle, add a `CHAPTERS` entry, mark its dot as built in `#rail`, and add its scene objects.

## Performance rules (the iPhone crash)

Mobile Safari ran out of graphics memory and reloaded when the world was built from huge layers. Keep it from coming back:

- World units are drawn at `U` = 0.2 CSS px (`--u` in CSS). **No element may be larger than about 2000 CSS px** in either direction; split anything bigger into tiles. Any CSS px value inside the world must be scaled (`calc(var(--u) * N)` or a percentage).
- Every object belongs to a **chapter group**. `cull()` sets far chapters and far objects to `display: none` each frame. New chapters must call `chapterGroup()` first.
- Touch devices get the `lite` class: no full-screen blend modes, backdrop blur, CSS filters, or sway animations inside big layers, and the star canvas is capped at 1.5x. Don’t add `filter`, `mix-blend-mode`, `backdrop-filter`, or `will-change` to world objects.
- The stage uses `lvh` and the camera frames to `svh`, so the iOS address bar never causes jumps.
- **Test on an iPhone 14 in Safari**: scroll from the top to the newest chapter and back up, three times in a row, with no crash and smooth motion. Before that, a Playwright pass with WebKit and iPhone 14 emulation at every size below is a good first check.

## Must keep working

- Regular navigation and the Games, About, and Join sections below the journey, so nobody has to scroll the whole world to find the Play button.
- The reduced motion version (`prefers-reduced-motion`), which jumps between chapter rest points.
- Every device, framed by aspect ratio rather than device names: test at 375 by 667, 390 by 844, 430 by 932, iPad portrait (820 by 1180) and landscape (1180 by 820), a narrow folded phone (about 360 by 780, and a short 390 by 400), the nearly square unfolded foldable (about 750 by 820), a landscape phone (844 by 390), and desktop. Folding, unfolding, and rotating must update live with no reload. The billboard, Shigost, the critters, the vine harp, and the signs stay in frame and readable.
- Tap targets at least 44 by 44 points (use `hit()` for small things), text readable without zooming, and safe areas respected on notched and Dynamic Island phones.
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
