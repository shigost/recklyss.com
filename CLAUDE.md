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

A scroll-driven, clickable journey through **one continuous 3D world**, from space to the beach. As visitors scroll, the camera follows Shigost through eight chapters:

The journey is a **true scroll adventure**: a simple story you can watch just by scrolling, and every other action (pausing, rewinding, moving the mouse, touching, and tapping) is rewarded with more about Shigost’s world and the creatures she meets.

1. **Outer space** (3D, and a preview of Alyssa's next game, a space explorer: little floating asteroids with Womps on them): hero billboard advertising Vibe Booth sits on a floating asteroid. Scrolling pulls back, Shigost fires her portal gun if tapped, jumps off, and parachutes down through the clouds (the camera swings above her to look down at the hills far below, around her side, and under her).
2. **Grassy hills** (3D): she lands among the painter, the easel, and the sheep choir, walks to the chime tree and rests, then hops into the jungle.
3. **Jungle** (3D): she rests by the vine harp in a misty clearing, then runs out of the jungle and leaps into the sunlight of the dunes while the camera soars over the canopy.
4. **Sand dunes** (3D): Shigost walks to the singing ridge and rests, then crosses the dunes and hops down the last big one.
5. **Beach** (3D): one continuous camera move over the last crest to the coast. Late-day light, waves, wet sand, tide pool, shells, and crabs. The far end leads into the water with a “The reef, coming soon” sign.
6. Reef (next)
7. Deep ocean
8. The island

The chapter order never changes. The space chapter is the quality bar and visual standard for every new 3D chapter.

When scrolling stops, each chapter plays an idle loop. Objects in each scene act as doors to other content (games, art, and so on). Build chapters one at a time, and keep earlier chapters working.

## Art direction

- **The whole journey is real 3D, matching Vibe Booth's look**: soft stylized lighting, gradients, depth, glow, and shadows. Cartoony and whimsical, but elevated. No flat fills and no bold outlines; 3D that keeps the charm of a 2D cartoon. New chapters are built in 3D too.
- Plants and critters are original and Seussian (curly stalks with pom bulbs, striped barrels, puff bushes, curly palms), never realistic cacti or real-world mascots. Sand is warm apricot and peach, not lemon yellow, and rest views keep sky or sea behind Shigost.
- **The old plan of hand-drawn 2D layers replacing SVG placeholders is retired.** The remaining SVG art (the 2D space, fall, hills, and jungle, kept as the fallback, and the small `#gostSym` Shigost in cards) is placeholder.
- The spirit is still **Studio Ghibli, Dr. Seuss, and Adventure Time**: soft skies and haze, curly whimsical shapes.
- Avoid anything that looks cheesy or clip-art: no bubbly fonts, no “Click me!” speech bubbles, no flat candy colors. Clickable things are marked with a soft dashed halo plus a small hint at the bottom of the screen.
- Font: Bricolage Grotesque (Google Fonts), often condensed.
- Shigost is referred to as **she**.

## The Recklyss family look (wompified)

- Alyssa's signature style: **soft, rounded, simple shapes with a matte finish, big glossy eyes, and stubby little limbs** (see Shigost's model and the Womps and Kikis in Vibe Booth's `app.js`). Every creature on the site follows it: the moon snail, puffsheep, lemur, parrot, dune hopper, crabs, and every Womp. The star whale stays as it is.
- In code: `matte(hex)` for bodies, `eyeM` and `glintM` for the glossy eyes, `glossyEyes()` for a pair of eyes on a 3D group, and `folk(parts)` with `eyePair(parts, ...)` to bake a critter into three draw calls (matte body, glossy eyes, glints).

## Womps

- **Womps** are the main characters of Alyssa's world: tall bean-shaped folks with stubby arms and legs and big glossy eyes. They're the crowd in Vibe Booth (unnamed there; their name is Womp), and the site reuses that design (`wompGeo()`, the same body profile as Vibe Booth's crowd).
- **They live everywhere**, in every chapter, space included. Each has its own personality: sizes range from as tall as the painter (about 880) down to Kiki size (about 100; Shigost is about 260), and colors and idle moods vary (`sway`, `wave`, `dance`, `cheer`).
- **The roster is `WOMPS`** (one entry per Womp: id, chapter, where it stands, height, color, and mood). Add, move, or recolor Womps there.
- **They're placeholders** until Alyssa builds them out. Each chapter draws its Womps with one shared set of InstancedMeshes (`wompSet`), so swapping in real models later means changing how a set is drawn, not the roster.
- **They're Shigost's crowd**: when a visitor plays a musical toy, nearby Womps cheer and hop (`s3.onToy`, called from `playedToy`).
- **The painter is a Womp artist** at her easel, in a beret, as tall as before.

## Who Shigost is

- Shigost is a **gost**, never a “ghost,” anywhere: copy, alt text, labels, comments, code, and this file. Definition, to use where it fits: “Shigost is a gost: a spirit who has crossed into a realm beyond, neither quite alive nor quite gone.”
- **Her real design** (placeholders must match it): a long, oversized white hoodie that reaches about her knees, hood up. Her white face sits inside a teardrop-shaped opening in the hood that points downward, with two big, round, glossy black eyes. Drawstrings hang from the neck, long sleeves mostly cover small hands, and she wears chunky white high-top sneakers. She is **not** a sheet ghost: no wavy hem.
- **Never put her on a yellow or gold background, and never near anything that resembles the Snapchat logo.** This covers card art, the billboard, the About art, and the world (the hills sky and sun are a rose haze, no tree near her is gold, and the jungle light is mint for this reason). Gold is fine for buttons and small accents away from her.
- She loves music, especially EDM, and wants to play it everywhere she explores.

## The game and Vibe Booth

- **Shigost** (the big game, in production) is a 3D explorer platformer and collectathon in the spirit of Banjo-Kazooie and Yooka-Laylee, with music at its heart. The DJ gameplay teaches real DJ skills. She travels to new environments, meets peoples and creatures, deals with changing weather, helps locals who then become her crowd and cheer at her shows, cleans up polluted places, and collects orbs, totems, notes, and sounds to build her gear and play her sets. There are environmental puzzles, character interactions, and boss fights.
- **Vibe Booth** (play.recklyss.com) is the playable teaser for the music side of the game: Shigost on her first tiny island. It will get a new name later and become an island in the full game.
- **The game’s other islands are private and not live.** Describe the kinds of worlds in general terms only. Never name, show, or link an individual island.

## Transitions between chapters

- The journey is one continuous world with **no hidden switches**: every chapter lives in the same 3D scene, so one camera flies from space to the beach. The camera swoops in every direction (up, down, sideways, toward and away) with big shifts in scale. Use a nested zoom (diving into something small to reveal the next place) only now and then.
- How the chapters connect: space to the fall, the camera follows her jump and swings above her to look down through the clouds; fall to hills, it circles under her and levels out as she lands; hills to jungle, it swings wide and low as she hops between the trees; jungle to dunes, it runs alongside her, rises with her leap, and soars over the canopy edge before diving to the dunes; dunes to beach, it rises over the last crest for a wide look at the coast, then dives down to the sand.
- Sky colors come from `skyFor(p, y)`, and light and fog from the lighting rig (`rig()`, presets `L_SPACE`, `L_FALL`, `L_HILLS`, `L_JUNGLE`, `L_DUNES`, and `L_BEACH`) blended by scroll position, so chapter moods change gradually.
- Camera keyframes live in `relayout()`. 3D stops carry `pitch` and `yaw`. `fit3()` frames 3D rest views (with an optional minimum zoom, used for the vine harp): tall screens crop the sides a little, look down a bit more, and give spare height to the sky above. `follow()` tracks Shigost while she moves.
- The old cover cloud (`HANDOFF`) and blinding sunlight (`#flash`, `J_FLASH`) only show in the 2D fallback now.

## Switching chapters back to 2D

- `LAND3D` (next to `HANDOFF` in `index.html`) turns on the 3D fall, hills, and jungle. To switch those chapters back to 2D, change it to `const LAND3D = false;`. To try the 2D version first without changing code, add `?land=2d` to the end of the address.
- With 2D on, the 2D fall, hills, and jungle (`chapterGroup(name, 'land')`) show again, the space chapter hands off to them through the cover cloud, and the jungle hands off to the 3D dunes through the blinding sunlight. The camera uses the 2D keyframes in the `!s3.L3` branch of `relayout()`.
- Devices without WebGL always get the full 2D world. Never delete the 2D chapters; they are the fallback.

## Recurring features for every chapter

- **A musical toy.** Music is the heart of Shigost's world. So far: the hills sheep choir (five puffsheep, each sings its own note of a C, D, E, G, A scale) and wind chimes on the curly chime tree, the jungle vine harp, the singing dune ridge, and the beach shell bells and tide pool. Anything with the class `vine`, a `data-freq`, and a `data-voice` can be tapped or strummed (`strummable()`); `tone(freq, voice)` has the voices `vine`, `dune`, `shell`, `bloop`, `chirp`, `clack`, `chime`, `baa`, and `windchime`. Keep strummable toys about 44 px apart on every screen (narrow screens get a closer rest view, like the harp close-up).
- **A cleanup moment.** Shigost keeps worlds clean: litter to tap away with a sparkle, a chime, and a thank-you (`litterAt()` and `toast()`). So far: the candy wrapper in the hills grass, the plastic bag snagged on a jungle vine, the half-buried can in the dunes, and three pieces of beach litter with a countdown.
- **One or two original critters** that react when tapped (the moon snail, painter, puffsheep, lemur, parrot, dune hopper, and two crabs).
- Soft dashed halos and a bottom hint mark what's tappable during each rest view, and every chapter ends by teasing the next one with a “coming soon” sign until that chapter exists.

## 3D: assets, setup, and loading

- **Assets come from Alyssa's game, but only from the public vibe-booth repo** (github.com/shigost/vibe-booth). **Never use anything from the unreleased game islands.** Right now that means only `assets/shigost.glb` and `assets/shigost.jpg`.
- **three.js r128** from cdnjs (`https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`) and **GLTFLoader 0.128.0** from jsDelivr (`https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/loaders/GLTFLoader.js`), exactly the versions Vibe Booth loads. Don't upgrade casually; r128 APIs (`sRGBEncoding`, `convertSRGBToLinear`) are assumed. They are injected after the page loads (`loadScript`), so the HTML hero never waits on them.
- **Colors**: as in Vibe Booth, every material, light, and vertex color goes through `C(hex)`, which is `new THREE.Color(hex).convertSRGBToLinear()`. Raw `ShaderMaterial`s (the sky gradient, stars, and portal) write sRGB straight out and use plain `THREE.Color`. Output is `sRGBEncoding` with ACES filmic tone mapping.
- **Shigost's model**: fetch `assets/shigost.glb`, parse with `GLTFLoader().parse`, put the scene in a body group scaled by `K` (3.2 here; Vibe Booth uses 0.04) and lifted `41.4*K` so her soles sit on the wrapper's origin. Texture: `flipY = false`, `encoding = sRGBEncoding`, applied to every mesh with white color, roughness 0.96, and metalness 0. She faces +z. Bones: `body`, `body_top0`, `neck`, `arm_left_*`/`arm_right_*` (`top`, `bot`, `hand`), `leg_left_top`, and `leg_right_top`. Clips are `sit`, `dance`, and `jump`; the site poses her procedurally with Vibe Booth's two-bone IK (`ik2`). Her left hand (screen right when she faces the camera) holds the portal gun.
- **How 3D lines up with the rest of the site**: `build3D()` makes a perspective camera that reads the same camera keyframes as the 2D world (`camAt`, `relayout`). World (x, y) is 3D (x, -y, 0) and the camera looks straight down -z, so anything on the z = 0 plane lands exactly where the 2D layer expects it. That's why the HTML hero, halos, and `hit()` tap areas still work over the 3D scene, and why framing adapts to every screen shape. Background objects sit at negative z.
- **`HANDOFF`** (0.56 of the space-and-hills span): before it, the space chapter's 2D tap areas (billboard, snail, Shigost, portal) sit over the 3D view (stage class `s3d`); after it, every tap target is a 3D hot spot (stage class `s3e`, the 2D world is hidden). In 3D nothing visible changes there. Only in the 2D fallback is it a real switch, hidden by a tall cloud on her path. The 3D sky uses the same `skyAt()` colors as the 2D `#sky`, and both star fields fade with `starAlpha()`.
- **Fallbacks**: the 2D art shows until 3D is ready, and stays if WebGL is missing or the context is lost. Stage classes: `s3d-ready` (hide 2D space art), `s3d` (space tap areas in use), `s3d-sg` (3D Shigost replaces the 2D one), `s3e` (3D hot spots in use), `s3e-ready` (hide the 2D dunes and beach), and `s3l` (the 3D fall, hills, and jungle are on, so their 2D versions and the sunlight flash are hidden).
- The billboard screen is a canvas texture laid out from the HTML hero's own text positions (`measureFace`), so the two match while the hero fades.
- **One scene, chapter groups.** `build3D()` makes `root` (one `THREE.Scene`) holding a group per chapter: `scene` (outer space), `LAND.fall`, `LAND.hills`, `LAND.jungle`, and `EARTH.group` (dunes and beach). `s3.update` hides groups far from the camera (by scroll position), so only nearby chapters are drawn. Lights, fog, the sky quad, the sun glow, sparkles, Shigost, and her ground shadow live on `root` and are shared.
- **Fall, hills, and jungle** (`buildLand()`): built shortly after load (or on demand). Ground heights come from `landH(x, z)`, which follows the 2D hills (`frontTop`) and jungle floor (`jFloor`) along z = 0 so 2D and 3D agree, rises into rolling hills behind, settles onto a flat plain toward the far edges (seen from high in the fall), and becomes exactly the dunes at `LAND_X1`, where the dunes terrain takes over. `groundH(x, z)` and `groundY(x)` cover the whole journey after the landing. Beats are in `HP` (scroll positions) plus `CHIME_X`, `REST_X`, `JUNGLE_OUT`, and `DUNES_IN`.
- **Dunes and beach** (`buildEarth()`): ground heights come from `earthH(x, z)` (height above `GE`; z = 0 is Shigost's path, negative is away from the camera), which the 3D terrain, Shigost's path (`earthAt`), and the 2D fallback all share. Beats are in `EP` and `EX`. The journey's scroll runs to `PMAX` (1.43).
- **3D tap targets** use `hotAt(target, radius, options)` (each chapter wraps it with its group: `hotH`, `hotJ`, or `hot`): a screen-space element positioned over the 3D object every frame, never smaller than 44 px, optionally taller than wide (`aspect`), with an optional halo. They hide with their chapter group and work at any camera angle.
- **Static decor is baked** into one draw call per material with `bake(parts)`; parts with a `sway` weight bend in the wind with `swayMat()` (grass, flowers, ferns, and hanging vines). Moving or tappable things stay separate meshes.

## Shigost's animations (shared library)

- Alyssa has a library of named animation clips on the same rig as her model (idle, walk, run, jump_start, jump, jump_fall, jump_end, crouch, crouch_walk, crawl, dance, lie_down, lying_down_idle, get_up_from_lying_down, sit, and more). They are **not in the repo yet**; don't look for them.
- The same clips will be shared by this site, Vibe Booth, and the game, so keep their names exactly as authored and load them by name.
- The site is ready for them: `SGA` in `build3D()` maps her states to clip names (`st-walk` to `walk`, `st-run` to `run` (out of the jungle), `st-land` to `idle`, `st-jump` to `jump`, `st-fall` to `jump_fall`), in every chapter from the landing to the beach. When a clip exists, it crossfades in (0.3 seconds) over the procedural pose; when it doesn't, the procedural pose (two-bone IK, breathing, looking around) shows. Load clips with `s3.loadClips(url)` from any GLB on the same rig (one file per clip or one library file both work). Clips play in place (root position tracks are dropped), because the journey moves her. Vibe Booth's own `sit`, `dance`, and `jump` are registered as `vb_*` so they never replace the site's poses by accident.
- When the files arrive: put them under `assets/anims/`, call `s3.loadClips` for the clips a chapter needs when that chapter gets near, and extend `SGA.map` for new states.

## Shigost's gaze and direction

- **Gaze** (`gazeFrame()` and `GZ`): moving the mouse, or touching and drawing on the screen, draws her head toward the pointer (`PTR`); scrolling makes her look where she's headed; both at once blend smoothly. When nobody steers her, she glances at nearby critters and Womps (the `GAZE` list, registered with `gazeAt()` and by every Womp), sometimes watching a butterfly and sometimes waving at a Womp. Head turns stay inside her neck's range (`NECK`) and ease in smoothly. With reduced motion her gaze stays calm and steady (no tracking).
- **Turning around**: she faces the way she's actually moving. Scrolling back turns her around (`moveDir`, passed as `s.dir`) with a quick, smooth turn, and scrolling forward turns her back. The 2D fallback Shigost flips too.

## Lore cards and the discovery journal

- **Lore**: every character (each Womp, each critter, and the painter) opens a small lore card when tapped (`meet(id)`), with a name and a short description. **Alyssa writes all the lore herself.** Every name and every piece of lore lives in the one `LORE` list; for now every card says “Lore coming in the next chapter.” Womp names there are placeholders for her to replace. Keep ids stable; the journal saves them.
- **Field journal** (`JOURNAL`, the round book button in the bottom-right corner): fills in as visitors meet characters, play the musical toys (`TOYS`, each toy tagged with `data-toy`), and clean up litter (`LITTER_SPOTS`, the last argument of `litterAt`), for example “You’ve met 6 of 28 characters.” It's saved in the visitor's browser (`localStorage`, key `recklyss-journal`) as plain JSON, `{ v, met, played, cleaned, updated }` with ids and times, so a later round can sync it to accounts and a public leaderboard (alongside the painting studio). `JOURNAL.data()` returns a copy of it.
- Both stay small and quiet: the lore card sits at the top left, doesn't block the world (so visitors can keep playing), and fades after a few seconds.

## Characters and interactions

- **Shigost**: see “Who Shigost is” above. In space she is the 3D model from Vibe Booth: she holds the portal gun and waves when idle, and tapping her fires the gun, eases the camera out, opens the portal, and shows the Space Explorer concept card. She jumps with her arms up and hangs from the parachute cords by her hands. The same 3D model carries her through every chapter: she lands, walks, hops, rests, runs out of the jungle, and leaps into the dunes. The 2D Shigost (separate SVG arm layers, stepping sneakers, idle loops) is only the fallback. The small `#gostSym` version is used in cards, About, and the billboard DJ.
- **Moon snail** on the asteroid hides in its shell when tapped. A **star whale** drifts in the background (unchanged, not wompified).
- **Floating asteroids** in space (`SPACE_SLOTS`) are a preview of the space explorer game: each is a slot with Womps standing on it. To drop in a 3D model of one of Alyssa's creatures later, set that slot's `model` to the `.glb` path and `height` to how tall it should stand; the placeholder Womps on that slot are replaced automatically. Shigost's portal and the Space Explorer card stay as they are.
- **The painter** in the hills (3D): a tall lavender Womp artist in a beret at her easel, painting with a long brush; tapping her makes a happy flourish. **Her canvas is a door**: tapping it shows the “Painting studio, coming soon” card (`studioCard`). Its position is `EASEL`.
- **Puffsheep** (3D sheep choir): five sheep of different sizes; each bounces and sings its own note.
- **Lemur** (3D) hangs by its tail from the harp limb and waves when tapped. The **parrot** perches on the same limb and chirps when tapped.
- **Dune hopper** in the dunes: a big-eared, lavender-cream critter that springs up and spins when tapped.
- Every critter tap also opens its lore card and adds it to the journal.
- **Crabs** on the beach (coral and pink) sidestep, and when tapped they raise their claws, clack, and scuttle off.
- The painter is inspired by Alyssa’s own character studies. In the 2D fallback, tapping her also opens the painting studio card.
- **Vine harp** in the jungle: seven vines hanging from a big limb; dragging across them plays notes (Web Audio, works with touch).

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
- `CHAPTERS` defines chapter names, scroll ranges, and rest points (used for the reduced motion version). Scroll progress `p` runs from 0 to `PMAX`.
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
- New 3D chapters: build lazily, keep the terrain grid modest (about 240 by 92 on desktop, smaller on phones), use bump textures for fine detail like sand ripples instead of more vertices, and fade far planes (like the sea) into the sky rather than letting their edges show.
- The crash test runs from the top to the end of the beach and back, three times.
- With the whole journey in 3D, watch total memory: chapters are built once (lazily) and reused, never rebuilt; grids stay modest (the land terrain is about 210 by 93, smaller on phones); textures are small canvases. If a real phone ever struggles, compare with `?land=2d` first, then switch with `LAND3D`.

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
- Build the **reef** chapter next (3D), continuing from the beach's waterline.
- Write the **lore** (names and descriptions) in `LORE`, including real names for the Womps.
- Build the Womps out properly and swap them in (see “Womps”), and drop creature models into the space slots (`SPACE_SLOTS`).
- **Accounts and a public leaderboard** built on the journal data, alongside the painting studio.
- **Painting studio** (next round): the painter's canvas (`EASEL`) becomes the door. Visitors tap it, the camera zooms into the canvas (add a camera stop framing it, the way the harp close-up works), they paint, and they submit to a public gallery with voting and a leaderboard. That needs a backend for storage, moderation, and spam protection, so plan it with Alyssa first.
- Drop in Shigost's shared animation clips when they're ready (see “Shigost's animations”).
- After the domain transfer: point recklyss.com at GitHub Pages and set up email forwarding for info@recklyss.com.
- About section copy is a draft.

## Working with Alyssa

- She’s a designer who ships and likes clear, step-by-step guidance for anything technical.
- In replies, use Oxford commas and never use em dashes.
- Avoid promising dates on the site. Use statuses like “in production” or “coming soon” instead.
