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

- `index.html` is the whole site: HTML, CSS, and JavaScript inline. No build step, no bundler.
- `assets/shigost.glb` and `assets/shigost.jpg`: Shigost's rigged 3D model and texture, copied unchanged from the vibe-booth repo.
- Old code from the Universe site is archived on Alyssa’s computer, **not** in this repo, because the repo is public. Don’t add archive files here.

## The vision

A scroll-driven, clickable journey through a world that is becoming **real 3D, one chapter at a time**. As visitors scroll, the camera follows Shigost through eight chapters:

1. **Outer space** (built in 3D): hero billboard advertising Vibe Booth sits on a floating asteroid. Scrolling pulls back, Shigost fires her portal gun if tapped, jumps off, and parachutes down. The 3D view hands off to the 2D world inside a cloud during the fall.
2. **Grassy hills** (built, still 2D): she lands, then walks right toward the jungle.
3. **Jungle** (built, still 2D): she hops into a misty jungle and rests by the vine harp.
4. Sand dunes (next)
5. Beach
6. Reef
7. Deep ocean
8. The island

When scrolling stops, each chapter plays an idle loop. Objects in each scene act as doors to other content (games, art, and so on). Build chapters one at a time, and keep earlier chapters working.

## Art direction

- **The site is moving to real 3D, chapter by chapter, matching Vibe Booth's look**: soft stylized lighting, gradients, depth, glow, and shadows. Cartoony and whimsical, but elevated. No flat fills and no bold outlines; 3D that keeps the charm of a 2D cartoon. Outer space is done; the hills and jungle are still 2D until their turn.
- **The old plan of hand-drawn 2D layers replacing SVG placeholders is retired.** The remaining SVG art (hills, jungle, the 2D space fallback, and the small `#gostSym` Shigost in cards) is placeholder until each chapter moves to 3D.
- The spirit is still **Studio Ghibli, Dr. Seuss, and Adventure Time**: soft skies and haze, curly whimsical shapes.
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

## 3D: assets, setup, and loading

- **Assets come from Alyssa's game, but only from the public vibe-booth repo** (github.com/shigost/vibe-booth). **Never use anything from the unreleased game islands.** Right now that means only `assets/shigost.glb` and `assets/shigost.jpg`.
- **three.js r128** from cdnjs (`https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`) and **GLTFLoader 0.128.0** from jsDelivr (`https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/loaders/GLTFLoader.js`), exactly the versions Vibe Booth loads. Don't upgrade casually; r128 APIs (`sRGBEncoding`, `convertSRGBToLinear`) are assumed. They are injected after the page loads (`loadScript`), so the HTML hero never waits on them.
- **Colors**: as in Vibe Booth, every material, light, and vertex color goes through `C(hex)`, which is `new THREE.Color(hex).convertSRGBToLinear()`. Raw `ShaderMaterial`s (the sky gradient, stars, and portal) write sRGB straight out and use plain `THREE.Color`. Output is `sRGBEncoding` with ACES filmic tone mapping.
- **Shigost's model**: fetch `assets/shigost.glb`, parse with `GLTFLoader().parse`, put the scene in a body group scaled by `K` (3.2 here; Vibe Booth uses 0.04) and lifted `41.4*K` so her soles sit on the wrapper's origin. Texture: `flipY = false`, `encoding = sRGBEncoding`, applied to every mesh with white color, roughness 0.96, and metalness 0. She faces +z. Bones: `body`, `body_top0`, `neck`, `arm_left_*`/`arm_right_*` (`top`, `bot`, `hand`), `leg_left_top`, and `leg_right_top`. Clips are `sit`, `dance`, and `jump`; the site poses her procedurally with Vibe Booth's two-bone IK (`ik2`). Her left hand (screen right when she faces the camera) holds the portal gun.
- **How 3D lines up with the rest of the site**: `build3D()` makes a perspective camera that reads the same camera keyframes as the 2D world (`camAt`, `relayout`). World (x, y) is 3D (x, -y, 0) and the camera looks straight down -z, so anything on the z = 0 plane lands exactly where the 2D layer expects it. That's why the HTML hero, halos, and `hit()` tap areas still work over the 3D scene, and why framing adapts to every screen shape. Background objects sit at negative z.
- **The 2D-to-3D handoff**: `HANDOFF` (0.56 of the space-and-hills span) is where the 3D view stops and the 2D world takes over, during the parachute fall. A tall 2D cloud is placed exactly on her path there so the swap is hidden. The 3D sky shader uses the same `skyAt()` colors as the 2D `#sky`, and both star fields fade with `starAlpha()`, so nothing pops.
- **Fallbacks**: the 2D space art (`art2d` class) shows until 3D is ready, and stays if WebGL is missing or the context is lost. Stage classes: `s3d-ready` (hide 2D space art), `s3d` (3D is rendering), and `s3d-sg` (3D Shigost replaces the 2D one).
- The billboard screen is a canvas texture laid out from the HTML hero's own text positions (`measureFace`), so the two match while the hero fades.

## Characters and interactions

- **Shigost**: see “Who Shigost is” above. In space she is the 3D model from Vibe Booth: she holds the portal gun and waves when idle, and tapping her fires the gun, eases the camera out, opens the portal, and shows the Space Explorer concept card. She jumps with her arms up and hangs from the parachute cords by her hands. After the handoff, the 2D Shigost (separate SVG arm layers, stepping sneakers, idle loops) takes over in the hills and jungle. The small `#gostSym` version is used in cards, About, and the billboard DJ.
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

## Performance rules for 3D

- Same crash test as above: a real iPhone 14 in Safari, top to the newest chapter and back, three times, no crash.
- Pixel ratio capped at 1.5 on phones and tablets (the `lite` class) and 2 on desktop, as in Vibe Booth.
- Keep geometry and textures modest: a few thousand vertices per object, `InstancedMesh` for repeats (the bulbs), canvas textures at most 1024 wide (768 on phones). No shadow maps; use the soft `contact()` blob shadows.
- Fake bloom with additive glow sprites (`glow()`), never post-processing.
- **Stop rendering when the 3D scene isn't on screen**: `s3.update` hides the canvas and skips `render()` once past `HANDOFF` or when the journey is scrolled away. The billboard screen texture only redraws while the HTML hero isn't covering it (20 fps on phones, 30 on desktop).
- The hero stays real HTML, so it shows instantly while three.js loads. The 2D space chapter is the fallback, so never delete it.
- Reduced motion: no camera flying. It jumps between calm rest views (the hero, the asteroid, the parachute in 3D, and then each chapter), and 3D idle motion, lasers, bulbs, and shooting stars hold still.
- Testing locally: the model loads with `fetch`, so open the site through a local server (Live Server, or any static server), not by double-clicking the file.

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
