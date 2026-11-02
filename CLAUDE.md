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
- `assets/anims/shigost-moves-space.glb` and `assets/anims/shigost-moves-world.glb`: trimmed bundles of her animation clips (see “Shigost's animations”).
- `assets/ad/island.mp4`, `island.webm`, and `island.jpg`: the billboard ad's island loop and its poster.
- `package.json`: local tools only (ffmpeg-static, for encoding video). The site still has no build step; `node_modules/` is ignored and never committed.
- `preview/parachute.html`: a design preview, not part of the journey (see “Design previews”). Never link it from the site.
- Old code from the Universe site is archived on Alyssa’s computer, **not** in this repo, because the repo is public. Don’t add archive files here.

## The vision

A scroll-driven, clickable journey through **one continuous 3D world**, from space down to the reef. As visitors scroll, the camera follows Shigost through eight chapters:

The journey is a **true scroll adventure**: a simple story you can watch just by scrolling, and every other action (pausing, rewinding, moving the mouse, touching, and tapping) is rewarded with more about Shigost’s world and the creatures she meets.

1. **Outer space** (3D, and a preview of Alyssa's next game, a space explorer: little floating asteroids with Womps on them): at the very top, the Vibe Booth ad fills the whole screen like a normal website hero; scrolling pulls back to reveal it was a billboard on an asteroid all along (the “woah” moment), and visitors can drag to spin all the way around the asteroid diorama. Scrolling on, Shigost fires her portal gun if tapped, jumps off, and her hoodie flies off her and inflates into a balloon that carries her down through the clouds (the camera swings above her to look down at the hills far below, around her side, and under her).
2. **Grassy hills** (3D): she lands among the painter, the easel, and the sheep choir, walks to the chime tree and rests, then hops into the jungle.
3. **Jungle** (3D): she rests by the vine harp in a misty clearing, then runs out of the jungle and leaps into the sunlight of the dunes while the camera soars over the canopy.
4. **Sand dunes** (3D): Shigost walks to the singing ridge and rests, then crosses the dunes and hops down the last big one.
5. **Beach** (3D): one continuous camera move over the last crest to the coast. Late-day light, waves, wet sand, tide pool, shells, and crabs. The far end leads into the water, with a “The reef, this way” sign by the waterline.
6. **Reef** (3D): she wades into the waves, her hood puffs up into a bubble helmet, and the camera follows her down through the surface in one move. She rests by the coral xylophone (a little octopus hides in the coral nook beside it), crosses the reef past the turtle, fish, and Womps in bubble helmets, rests on a soft moss bed by the glowing anemones, and ends at the reef's edge, where the floor drops away into the deep ocean beside a “The deep ocean, coming soon” sign.
7. Deep ocean (next)
8. The island

The chapter order never changes. The space chapter is the quality bar and visual standard for every new 3D chapter.

When scrolling stops, each chapter plays an idle loop. Objects in each scene act as doors to other content (games, art, and so on). Build chapters one at a time, and keep earlier chapters working.

## Art direction

- **The whole journey is real 3D, matching Vibe Booth's look**: soft stylized lighting, gradients, depth, glow, and shadows. Cartoony and whimsical, but elevated. No flat fills and no bold outlines; 3D that keeps the charm of a 2D cartoon. New chapters are built in 3D too.
- Plants and critters are original and Seussian (curly stalks with pom bulbs, striped barrels, puff bushes, curly palms, pom corals, and lattice fans), never realistic cacti or real-world mascots. Sand is warm apricot and peach, not lemon yellow, and rest views keep sky or sea behind Shigost.
- **The old plan of hand-drawn 2D layers replacing SVG placeholders is retired.** The remaining SVG art (the 2D space, fall, hills, and jungle, kept as the fallback, and the small `#gostSym` Shigost in cards) is placeholder.
- The spirit is still **Studio Ghibli, Dr. Seuss, and Adventure Time**: soft skies and haze, curly whimsical shapes.
- Avoid anything that looks cheesy or clip-art: no bubbly fonts, no “Click me!” speech bubbles, no flat candy colors. Clickable things are marked with a soft dashed halo plus a small hint at the bottom of the screen.
- Font: Bricolage Grotesque (Google Fonts), often condensed.
- Shigost is referred to as **she**.

## The Recklyss family look (wompified)

- Alyssa's signature style: **soft, rounded, simple shapes, matte everything, big flat matte black eyes like Shigost's (no shine, highlights, or reflections), and stubby little limbs** (see Shigost's model and the Womps and Kikis in Vibe Booth's `app.js`). Every creature on the site follows it: the moon snail, puffsheep, lemur, parrot, dune hopper, crabs, sea turtle, little octopus, reef fish, and every Womp. The star whale stays as it is.
- In code: `matte(hex)` for bodies, `eyeM` for the matte eyes, `matteEyes()` for a pair of eyes on a 3D group, and `folk(parts)` with `eyePair(parts, ...)` to bake a critter into two draw calls (matte body and eyes). `spirit(material)` adds the soft lavender rim. (three.js r128 has no `output_fragment` shader chunk, so shader patches that change the final color hook `OUT_FRAG`, the line that writes it. Before this round `spirit()` hooked the missing chunk, so the rim never showed; it does now.)

## Spirits, colors, and readability

- **Gosts and Womps are beings of Alyssa's own invented spirit realm.** Keep them clearly separate from any real ancestral spirit traditions, including CHamoru ones (see Vibe Booth's guidelines: never depict taotaomo'na or ancestral skulls).
- **All wompified humanoids are white** (they're spirits), unless Alyssa says otherwise: every Womp, and the painter (her beret stays lavender).
- **All animals are white too** (animal spirits): the moon snail, puffsheep, lemur, parrot, dune hopper, butterflies, and on the reef the sea turtle, the little octopus, and the reef fish. Exceptions: the crabs keep their coral and pink, and the purple bird flock in the fall stays as it is. The star whale is unchanged.
- **Readability**: white characters must stay readable against white or pale things (clouds, sand, white plants). Every spirit material gets a soft lavender rim at its silhouette (`spirit()`), and every character stands on a soft contact shadow.
- **When characters vary in color in the future, tie colors to elements and materials** (gemstone, coral, moss, stone, light), never to human skin tones.
- **Plants**: each area keeps its plants within one color family: the hills trees are the rose family (under the rose haze), the dunes plants are the sage family, the beach plants are greens, the reef is the aqua and teal family (corals and sponges, with sea greens for the kelp and seagrass), and the jungle stays green and colorful for now. Exceptions are flowers and glowing alien plants, which can be more colorful as long as they follow a palette tailored to their area (the space crystals and mushrooms: teal, violet, and rose; the jungle's living light: mint, violet, magenta, lime, and sky blue; the reef's accent: glowing pink and violet flowers, pom bulbs, polyps, and anemones). The reef stays distinct from the green jungle and the peach dunes, and leads toward the darker blues of the deep ocean.

## Brand palette (UI)

- **Orange, white, and purple.** Buttons are orange (`--orange` #ff8a3d, pressed edge `--orange-deep`), labels and status chips are purple (`--purple` #8b6cff) with white text, and text on dark is white. The lilac (`--lilac`) is a soft accent.
- **Subtle neon**: thin glowing edges, techy but minimal (`--neon-orange` on buttons and the active rail dot, `--neon-purple` on chips, and faint purple glows on the nav, tips, cards, and journal). Never yellow or gold for UI.

## Womps

- **Womps** are the main characters of Alyssa's world: tall bean-shaped folks with stubby arms and legs and big matte black eyes. They're the crowd in Vibe Booth (unnamed there; their name is Womp), and the site reuses that design (`wompGeo()`, the same body profile as Vibe Booth's crowd).
- **They live everywhere**, in every chapter, space included. Each has its own personality: sizes range from as tall as the painter (about 880) down to Kiki size (about 100; Shigost is about 260), and idle moods vary (`sway`, `wave`, `dance`, `cheer`). For now they're all white spirits; the `color` field in `WOMPS` is there for element-based colors later.
- **The roster is `WOMPS`** (one entry per Womp: id, chapter, where it stands, height, color, mood, and `helmet` for a little bubble helmet under water, drawn with the rest of the set). Add, move, or recolor Womps there.
- **They're placeholders** until Alyssa builds them out. Each chapter draws its Womps with one shared set of InstancedMeshes (`wompSet`), so swapping in real models later means changing how a set is drawn, not the roster.
- **They're Shigost's crowd**: when a visitor plays a musical toy, nearby Womps cheer and hop (`s3.onToy`, called from `playedToy`).
- **The painter is a Womp artist** at her easel, in a beret, as tall as before.

## Who Shigost is

- Shigost is a **gost**, never a “ghost,” anywhere: copy, alt text, labels, comments, code, and this file. Definition, to use where it fits: “Shigost is a gost: a spirit who has crossed into a realm beyond, neither quite alive nor quite gone.”
- **Her real design** (placeholders must match it): a long, oversized white hoodie that reaches about her knees, hood up. Her white face sits inside a teardrop-shaped opening in the hood that points downward, with two big, round, matte black eyes (no highlights). Drawstrings hang from the neck, long sleeves mostly cover small hands, and she wears chunky white high-top sneakers. She is **not** a sheet ghost: no wavy hem.
- **Never put her on a yellow or gold background, and never near anything that resembles the Snapchat logo.** This covers card art, the billboard, the About art, and the world (the hills sky and sun are a rose haze, no tree near her is gold, and the jungle light is mint for this reason). UI buttons are orange (see “Brand palette”), never gold.
- She loves music, especially EDM, and wants to play it everywhere she explores.

## Her hoodie is her tool

Her hoodie is her one magic tool for surviving everywhere she explores. Each new place can give it a new trick.

- **Two tricks for falling**, picked by the beat of the journey (`shigostAt()` and `earthAt()`):
  - **The hoodie flies off** (long falls and flying: the big drop from space, and any long falls or flying in future chapters; any beat with `s: 'st-chute'`). At the pop her hoodie flies up off her and inflates into a big stretchy balloon (the hood with its teardrop opening, the pocket, the ribbed hem, and dangling drawstrings), and she hangs below in her spirit body, holding its long stretchy sleeves with ribbed cuffs. It billows and wobbles as it slows her fall. On landing in the hills it deflates, floats back down onto her, and she wriggles back into it, then carries on in her normal model. A small poof of sparkles hides each swap (`burst()`). In code: `hoodieBalloon()` (built the first time it opens), `liveTube()` for the sleeves, and the `chute` block in `poseShigost()` (`HD` holds whether the hoodie is off). This replaced the old double-hoodie parachute.
  - **The hem flares out** (short, safe drops: the hop into the jungle, the three hops down the big dune, and any short drops in future chapters; any airborne beat with `d: 1`). The hoodie stays on her shoulders and arms while the bottom flares out into a soft billowing cup with gathered lobes, showing her spirit legs underneath, and it settles back down as she lands. Its rolled edge stays below her face, and the cup stays mostly upright as she leans into the hop, so it always reads as catching the air. In code: `FLARE`, `buildFlare()` (measures her hoodie's waist and hem at load), and `hemShape()`. Her hoodie's skirt is hidden with a per-vertex mask (`cut`) while the flare stands in for it; the model itself is never cut apart.
  - To use a trick in a new chapter, give the beat `s: 'st-chute'` for a long fall, or `s: 'st-jump'` with `d: 1` for a short drop.
  - Reduced motion: no poofs, no springy pop, and no billowing; the bodies cross-fade and the balloon and the flare ease open and closed.
  - The 2D fallback still draws its own 2D hoodie balloon (`.chute` in the `#shigost` SVG) over the 2D Shigost, and has no flared hem yet.
- **The bubble helmet** (under water): her hood puffs up into a clear bubble around her head. The hood's edge stays as a soft fabric collar, with the hood's seam over the top and the drawstrings at the front, so it reads as the same hoodie trick. Her matte black eyes show clearly through it (the bubble is nearly clear in the middle, rimmed at the edges, with one small highlight away from her eyes). It inflates with a springy pop when her head goes under (`s.w` from `reefAt()`) and deflates with a puff of bubbles when she leaves the water. In code: `helm`, `bubbleM()` (the Womps' little helmets use it too), and `measureHead()`, which fits the helmet to her model's own head once at load. The 2D fallback adds a bubble to the 2D Shigost (`#shigost.uw .bubble`).

## Her spirit body

- Under her hoodie, Shigost has a **spirit body**: white, matte, Womp-like, with her own arms, bare human-shaped feet, and a cute rounded cartoon butt (no other anatomy). It shows when her hoodie flies off, and its legs show under the flared hem.
- Alyssa hand-built the real one in VR, but it isn't rigged yet. Until then a **placeholder** is built in code, in the “SHIGOST'S SPIRIT BODY” block of `index.html` (`spiritPlaceholder()`): simple rounded shapes (a big round head with her matte black eyes, a bean of a body, stubby arms with small hands and thumbs, legs, five-toed feet, and the butt) laid out on her own skeleton and baked into one skinned mesh (one draw call), bound to the same bones as her hoodie model. So every clip, her gaze, and the IK drive it exactly as they drive her.
- **To swap in the real body**: rig it on the same skeleton as `assets/shigost.glb` (same bone names, rest pose, and scale), export it as a `.glb`, put it in `assets/`, and set `SPIRIT_BODY` (in that block) to its path, for example `'assets/shigost-spirit.glb'`. Its skinned meshes are re-bound to her bones by name, given the matte spirit material (`spiritMat()`: the lavender rim, kept off the eyes), and the placeholder is skipped. If the file fails to load, the placeholder comes back. Under the flared hem only the parts below her waist show (`SPIRIT.waist`, in her model's units), so keep the real body at the same scale.
- Her hoodie model and the spirit body never show at once, except under the flared hem (`setBodies()`). Never cut her current model apart; swap between the two instead.

## The game and Vibe Booth

- **Shigost** (the big game, in production) is a 3D explorer platformer and collectathon in the spirit of Banjo-Kazooie and Yooka-Laylee, with music at its heart. The DJ gameplay teaches real DJ skills. She travels to new environments, meets peoples and creatures, deals with changing weather, helps locals who then become her crowd and cheer at her shows, cleans up polluted places, and collects orbs, totems, notes, and sounds to build her gear and play her sets. There are environmental puzzles, character interactions, and boss fights.
- **Vibe Booth** (play.recklyss.com) is the playable teaser for the music side of the game: Shigost on her first tiny island. It will get a new name later and become an island in the full game.
- **The game’s other islands are private and not live.** Describe the kinds of worlds in general terms only. Never name, show, or link an individual island.

## Transitions between chapters

- The journey is one continuous world with **no hidden switches**: every chapter lives in the same 3D scene, so one camera flies from space to the beach. The camera swoops in every direction (up, down, sideways, toward and away) with big shifts in scale. Use a nested zoom (diving into something small to reveal the next place) only now and then.
- How the chapters connect: space to the fall, the camera follows her jump and swings above her to look down through the clouds; fall to hills, it circles under her and levels out as she lands; hills to jungle, it swings wide and low as she hops between the trees; jungle to dunes, it runs alongside her, rises with her leap, and soars over the canopy edge before diving to the dunes; dunes to beach, it rises over the last crest for a wide look at the coast, then dives down to the sand; beach to reef, it follows her as she wades in and goes down through the surface with her, from the open sea's side so the shore stays behind her.
- Sky colors come from `skyFor(p, y)`, and light and fog from the lighting rig (`rig()`, presets `L_SPACE`, `L_FALL`, `L_HILLS`, `L_JUNGLE`, `L_DUNES`, `L_BEACH`, and `L_REEF`) blended by scroll position, so chapter moods change gradually. Under water the sky dome and fog take the water's color (`reefSky(p)`: bright aqua toward the surface, teal haze all around, deepening toward the drop-off), blended by the camera's own height against the surface (`RIG.uw`), so the switch happens exactly as the camera dips under.
- Camera keyframes live in `relayout()`. 3D stops carry `pitch` and `yaw`. For the dive, `sub(q, height, yaw)` sets the camera's height against the water (positive above it, negative below), and `uw()` keeps every underwater view below the surface and above the sea floor on any screen shape. `fit3()` frames 3D rest views (with an optional minimum zoom, used for the vine harp): tall screens crop the sides a little, look down a bit more, and give spare height to the sky above. `follow()` tracks Shigost while she moves.
- The old cover cloud (`HANDOFF`) and blinding sunlight (`#flash`, `J_FLASH`) only show in the 2D fallback now.

## Switching chapters back to 2D

- `LAND3D` (next to `HANDOFF` in `index.html`) turns on the 3D fall, hills, and jungle. To switch those chapters back to 2D, change it to `const LAND3D = false;`. To try the 2D version first without changing code, add `?land=2d` to the end of the address.
- With 2D on, the 2D fall, hills, and jungle (`chapterGroup(name, 'land')`) show again, the space chapter hands off to them through the cover cloud, and the jungle hands off to the 3D dunes through the blinding sunlight. The camera uses the 2D keyframes in the `!s3.L3` branch of `relayout()`.
- Devices without WebGL always get the full 2D world. Never delete the 2D chapters; they are the fallback.

## Recurring features for every chapter

- **A musical toy.** Music is the heart of Shigost's world. So far: the hills sheep choir (five puffsheep, each sings its own note of a C, D, E, G, A scale) and wind chimes on the curly chime tree, the jungle vine harp, the singing dune ridge, the beach shell bells and tide pool, and on the reef the coral xylophone and the glowing anemones (they lean toward a finger or the mouse, and a mouse brushing through them plays them too). Anything with the class `vine`, a `data-freq`, and a `data-voice` can be tapped or strummed (`strummable()`); `tone(freq, voice)` has the voices `vine`, `dune`, `shell`, `bloop`, `chirp`, `clack`, `chime`, `baa`, `windchime`, `xylo`, and `anemone`. Keep strummable toys about 44 px apart on every screen (narrow screens get a closer rest view, like the harp close-up and the reef's two close-ups).
- **A cleanup moment.** Shigost keeps worlds clean: litter to tap away with a sparkle, a chime, and a thank-you (`litterAt()` and `toast()`). So far: the candy wrapper in the hills grass, the plastic bag snagged on a jungle vine, the half-buried can in the dunes, three pieces of beach litter with a countdown, and the fishing net tangled on a reef coral.
- **One or two original critters** that react when tapped (the moon snail, painter, puffsheep, lemur, parrot, dune hopper, two crabs, the sea turtle, the little octopus, and a school of reef fish).
- Soft dashed halos and a bottom hint mark what's tappable during each rest view, and every chapter ends by teasing the next one with a “coming soon” sign until that chapter exists.

## 3D: assets, setup, and loading

- **Assets come from Alyssa's game, but only from the public vibe-booth repo** (github.com/shigost/vibe-booth). **Never use anything from the unreleased game islands.** Right now that means only `assets/shigost.glb` and `assets/shigost.jpg`, plus her trimmed animation bundles.
- **The master files live in the private `shigost-assets` repo** (on Alyssa's computer at `Recklyss Studios/shigost-assets`): her model, texture, and the full animation library, shared by this site, Vibe Booth, and the games. **This public site only ever contains trimmed clips** built from it, never the master files.
- **three.js r128** from cdnjs (`https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`) and **GLTFLoader 0.128.0** from jsDelivr (`https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/loaders/GLTFLoader.js`), exactly the versions Vibe Booth loads. Don't upgrade casually; r128 APIs (`sRGBEncoding`, `convertSRGBToLinear`) are assumed. They are injected after the page loads (`loadScript`), so the HTML hero never waits on them.
- **Colors**: as in Vibe Booth, every material, light, and vertex color goes through `C(hex)`, which is `new THREE.Color(hex).convertSRGBToLinear()`. Raw `ShaderMaterial`s (the sky gradient, stars, and portal) write sRGB straight out and use plain `THREE.Color`. Output is `sRGBEncoding` with ACES filmic tone mapping.
- **Shigost's model**: fetch `assets/shigost.glb`, parse with `GLTFLoader().parse`, put the scene in a body group scaled by `K` (3.2 here; Vibe Booth uses 0.04) and lifted `41.4*K` so her soles sit on the wrapper's origin. Texture: `flipY = false`, `encoding = sRGBEncoding`, applied to every mesh with white color, roughness 0.96, and metalness 0. She faces +z. Bones: `body`, `body_top0`, `neck`, `arm_left_*`/`arm_right_*` (`top`, `bot`, `hand`), `leg_left_top`, and `leg_right_top`. Clips are `sit`, `dance`, and `jump`; the site poses her procedurally with Vibe Booth's two-bone IK (`ik2`). Her left hand (screen right when she faces the camera) holds the portal gun.
- **How 3D lines up with the rest of the site**: `build3D()` makes a perspective camera that reads the same camera keyframes as the 2D world (`camAt`, `relayout`). World (x, y) is 3D (x, -y, 0) and the camera looks straight down -z, so anything on the z = 0 plane lands exactly where the 2D layer expects it. That's why the HTML hero, halos, and `hit()` tap areas still work over the 3D scene, and why framing adapts to every screen shape. Background objects sit at negative z.
- **`HANDOFF`** (0.56 of the space-and-hills span): before it, the space chapter's 2D tap areas (billboard, snail, Shigost, portal) sit over the 3D view (stage class `s3d`); after it, every tap target is a 3D hot spot (stage class `s3e`, the 2D world is hidden). In 3D nothing visible changes there. Only in the 2D fallback is it a real switch, hidden by a tall cloud on her path. The 3D sky uses the same `skyAt()` colors as the 2D `#sky`, and both star fields fade with `starAlpha()`.
- **Fallbacks**: the 2D art shows until 3D is ready, and stays if WebGL is missing or the context is lost. Stage classes: `s3d-ready` (hide 2D space art), `s3d` (space tap areas in use), `s3d-sg` (3D Shigost replaces the 2D one), `s3e` (3D hot spots in use), `s3e-ready` (hide the 2D dunes and beach), and `s3l` (the 3D fall, hills, and jungle are on, so their 2D versions and the sunlight flash are hidden).
- The billboard screen is a canvas texture laid out from the HTML hero's own text positions (`measureFace`), so the two match while the hero fades.
- **One scene, chapter groups.** `build3D()` makes `root` (one `THREE.Scene`) holding a group per chapter: `scene` (outer space), `LAND.fall`, `LAND.hills`, `LAND.jungle`, `EARTH.group` (dunes and beach), and `REEF.group`. `s3.update` hides groups far from the camera (by scroll position), so only nearby chapters are drawn. Lights, fog, the sky dome, the sun glow, sparkles, Shigost, her ground shadow, her bubble helmet, and the sea (`EARTH.sea`, shared by the beach and the reef) live on `root` and are shared.
- **Fall, hills, and jungle** (`buildLand()`): built shortly after load (or on demand). Ground heights come from `landH(x, z)`, which follows the 2D hills (`frontTop`) and jungle floor (`jFloor`) along z = 0 so 2D and 3D agree, rises into rolling hills behind, settles onto a flat plain toward the far edges (seen from high in the fall), and becomes exactly the dunes at `LAND_X1`, where the dunes terrain takes over. `groundH(x, z)` and `groundY(x)` cover the whole journey after the landing. Beats are in `HP` (scroll positions) plus `CHIME_X`, `REST_X`, `JUNGLE_OUT`, and `DUNES_IN`.
- **Dunes and beach** (`buildEarth()`): ground heights come from `earthH(x, z)` (height above `GE`; z = 0 is Shigost's path, negative is away from the camera), which the 3D terrain, Shigost's path (`earthAt`), and the 2D fallback all share. Beats are in `EP` and `EX`. The journey's scroll runs to `PMAX` (1.64).
- **The reef** (`buildReef()`): built in an idle moment once the journey reaches the beach (or on demand), drawn from p 1.37 (the beach's group is hidden after 1.47). Its floor comes from `reefH(x, z)`, which `earthH()` blends into past x 30300, so Shigost's path, the 3D floor, and the 2D fallback agree: it slopes down to `REEF_D` (1250 below the surface), with ridges rising behind the path (always under water), a gentle dip in front so nothing blocks the camera, and the drop-off at `DROP_X`. Beats are in `RP` (scroll positions) and `RFX` (her rest spots). The sea's shader has an underside: a bright, rippling window straight up that fades into the water's haze. `underwater(material)` gives the floor, rocks, corals, and plants the depth tint and soft caustics. Corals, rocks, and fish are `InstancedMesh`es (one per coral shape, one per fish school plus its eyes); plants and the glowing accent are baked and sway with `swayMat()`; light shafts and bubbles show only under water.
- **3D tap targets** use `hotAt(target, radius, options)` (each chapter wraps it with its group: `hotH`, `hotJ`, or `hot`): a screen-space element positioned over the 3D object every frame, never smaller than 44 px, optionally taller than wide (`aspect`), with an optional halo. They hide with their chapter group and work at any camera angle.
- **Static decor is baked** into one draw call per material with `bake(parts)`; parts with a `sway` weight bend in the wind with `swayMat()` (grass, flowers, ferns, and hanging vines). Moving or tappable things stay separate meshes.

## Shigost's animations (shared library)

- Her 40 clips (plus the rig export) live in the private **shigost-assets** repo, all on the same rig as `assets/shigost.glb` (the bone names match exactly; no remapping). Its README lists every clip, what it is, and which projects use it. The originals she exported (in `Recklyss Studios/Shigost/GLB Animations`) are read only: never move, rename, or delete anything there.
- **The site ships two trimmed bundles** built by `tools/build-site-anims.mjs` in shigost-assets: `shigost-moves-space.glb` (idle, crouch, jump_start, jump, jump_fall, jump_end, and dance; about 95 KB, loaded with her model) and `shigost-moves-world.glb` (walk, run, lie_down, lying_down_idle, get_up_from_lying_down, crouch_walk, sit, sitting_idle, get_up_from_sitting, sitting_eat, and zombie_walk; about 165 KB, loaded as the journey nears the hills). Only animation data: no meshes or textures, no scale tracks, no root motion (the journey moves her; `body` translation stays for sitting and lying, except in the airborne clips, where the journey's arc lifts her), no tracks that never leave her rest pose, fewer keyframes, and 16-bit rotations.
- **Never on the site**: the combat clips (axe, sword, punches, kicks, parries, and die), `walk_back` (scrolling back uses the turnaround instead), `crawl`, `eat`, `get_up_from_crouch`, and `sit_down_to_drive`. Those are for the game.
- **The clip system** (`SGA` in `build3D()`): `SGA.play(name, once)` crossfades to a clip (0.3 seconds), looping or playing once and holding its last frame. Where a clip isn't loaded yet, the procedural pose shows (two-bone IK, breathing, stepping). On top of any clip, three layers always apply: her head follows the gaze, the portal gun arm aims at the portal, and her hands hold the balloon's sleeves. Vibe Booth's own `sit`, `dance`, and `jump` (inside her model) are registered as `vb_*` so they never replace the site's clips.
- **Which clip, by chapter** (`chooseClip()`, the “brain”, using the chapter, scroll speed, idle time, and toys):
  - Space: `idle` on the asteroid (with the portal gun), `crouch` at the edge, then `jump_start` and `jump` for the leap. Tapping her still fires the portal gun.
  - The fall: `jump_fall` under the balloon, in her spirit body, hands on the sleeves; `jump_end` when she lands in the hills, then she wriggles back into her hoodie.
  - Hills: `walk` toward the jungle. When the visitor stops scrolling, she lies down to watch the clouds (`lie_down`, then `lying_down_idle`) and gets up (`get_up_from_lying_down`) when scrolling resumes.
  - Jungle: `jump_start`, `jump`, and `jump_end` for the hop in; `crouch_walk` under the low mossy bough (`LOW_BOUGHS`); `dance` while the vine harp plays; `run` out to the dunes.
  - Dunes: `run` down the big dune toward the beach. When idle, she sits (`sit`, then `sitting_idle`) and gets up (`get_up_from_sitting`) when scrolling resumes.
  - Beach: when idle, she sits for a snack (`sit`, then `sitting_eat`); `dance` while the shell bells play.
  - Reef: slow, floaty steps on the sea floor (`walk` at a slower speed, with a gentle hop now and then from `reefAt()`). When the visitor scrolls fast, she kicks off into a glide above the reef and settles back down when the scrolling slows (see “Swimming” below). When idle she sits, or at the second rest lies down on the moss bed to watch the fish and the light; `dance` while the coral xylophone or the anemones play.
  - Anywhere after space: tapping her makes her do a quick happy dance.
  - Walking blends to `run` by scroll speed (with a little hysteresis), and every walk-type clip's speed follows how fast she's actually moving, so her steps keep pace with the scroll.
  - **Easter egg**: scroll backwards very slowly for a few seconds and she switches to `zombie_walk`, until the visitor speeds up or stops. Skipped with reduced motion.
  - Reduced motion: calm idles only (no dancing loops, no lying or sitting transitions).
- **Swimming** (`SWIM` and `BR.swim`): she has no swim clip yet, so the glide is posed procedurally on top of an existing clip: `jump_fall` with her body tipped forward (`SWIM.pitch`), lifted `SWIM.lift` above the floor, a gentle flutter kick, and her arms reaching ahead. **To use a real swim clip**: animate `swim` on her rig in shigost-assets, add it to the world bundle in `tools/build-site-anims.mjs`, and rebuild. The brain plays it by name as soon as it loads, and the procedural kick and arms step aside; if the clip is animated lying flat already, leave `SWIM.clipPitch` at 0; otherwise set it to how far she should tip forward.
- **To add or swap a clip**: animate it on the same rig in shigost-assets, add it to a bundle in `tools/build-site-anims.mjs`, run `node tools/build-site-anims.mjs "../recklyss.com/assets/anims"`, then use it by name in `chooseClip()` (a looping clip returns `{ name }`, a one-time clip `{ name, once: true }`, and `speed` sets its playback rate). Swapping a clip with the same name only needs the rebuild.
- `?debug` at the end of the address adds `window.recklyssDebug()`, which reports her current clip, posture, speed, glide (`swim`), helmet (`helm`), whether the camera is under water (`uw`), and how far her head points from the gaze target (handy for testing).

## Shigost's gaze and direction

- **Gaze** (`gazeFrame()` and `GZ`): moving the mouse, or touching and drawing on the screen, draws her head toward the pointer (`PTR`); scrolling makes her look where she's headed; both at once blend smoothly. When nobody steers her, she glances at nearby critters and Womps (the `GAZE` list, registered with `gazeAt()` and by every Womp), sometimes watching a butterfly and sometimes waving at a Womp. Head turns stay inside her neck's range (`NECK.range`) and ease in smoothly. With reduced motion her gaze stays calm and steady (no tracking).
- **How the gaze is applied** (`lookLayer()`): in world space, after the current clip has posed her, it turns her neck from wherever the clip holds her head toward the target, limited to her neck's range. It never guesses the neck bone's axes (the old version did, which made her look the opposite way once she turned), so she always looks toward the mouse or finger, in every direction, whichever way she's facing, under water and mid-glide too.
- **Turning around**: she faces the way she's actually moving. Scrolling back turns her around (`moveDir`, passed as `s.dir`) with a quick, smooth turn, and scrolling forward turns her back. The 2D fallback Shigost flips too.

## Lore cards and the discovery journal

- **Lore**: every character (each Womp, each critter, and the painter) opens a small lore card when tapped (`meet(id)`), with a name and a short description. **Alyssa writes all the lore herself.** Every name and every piece of lore lives in the one `LORE` list; for now every card says “Lore coming in the next chapter.” The reef added the sea turtle, the little octopus, the reef fish, and two Womps (the reef diver and the little bubble Womp). Womp names there are placeholders for her to replace. Keep ids stable; the journal saves them.
- **Field journal** (`JOURNAL`, the round book button in the bottom-right corner): fills in as visitors meet characters, play the musical toys (`TOYS`, each toy tagged with `data-toy`), and clean up litter (`LITTER_SPOTS`, the last argument of `litterAt`), for example “You’ve met 6 of 28 characters.” It's saved in the visitor's browser (`localStorage`, key `recklyss-journal`) as plain JSON, `{ v, met, played, cleaned, updated }` with ids and times, so a later round can sync it to accounts and a public leaderboard (alongside the painting studio). `JOURNAL.data()` returns a copy of it.
- Both stay small and quiet: the lore card sits at the top left and doesn't block the world (so visitors can keep playing).
- **Calm pop-ups** (`meet()` and `toast()`): tapping a character on purpose always shows its lore card. Characters found while playing a toy (like the sheep choir) get a card only for the first couple of discoveries, and never back to back; after that the journal button's orange counter quietly says “new” instead. Every card fades away on its own after about four and a half seconds (no need to tap ×). Achievement messages (litter thank-yous) have a cooldown, so they never stack up or come back to back.

## The opening: the ad is the hero

- At the very top, the camera is zoomed in so far that the Vibe Booth ad fills the entire screen on every device (no frame, bulbs, or posts), like a normal website hero. Scrolling pulls back to reveal the billboard on its asteroid.
- The ad is the HTML hero (`#heroOverlay`, `faceHTML`): it's the billboard's face clipped to the screen, so it starts as the whole screen and settles into the billboard's 16:9 shape as the camera pulls back (`cover` and `zCover` in `relayout()`, `kFull` in the frame). Its layout uses its own width and height (`cqw`, `cqh`), so it flows smoothly from any screen shape: on tall screens the copy spans the width and Shigost dances big below it. Text stays real HTML, so it stays crisp. While it fills the screen (`adfull`), phones show the whole ad; the call to action below the billboard appears once it has settled.
- The livelier ad: two bass speakers bump to a 120 BPM beat, the cartoon Shigost dances, and an island loop plays behind everything. The 3D billboard screen (`drawScreen`) draws the same video, speakers, and dancing Shigost once the HTML ad fades into it.
- **The billboard video**: a 10 second, muted, seamless loop pre-rendered from Vibe Booth's island (stepping its clock frame by frame in a browser, then crossfading the last two seconds into the first two). Files: `assets/ad/island.mp4` (H.264, about 745 KB, listed first; plays everywhere, older iPhones included), `assets/ad/island.webm` (VP8, about 1 MB, the fallback), and the poster `assets/ad/island.jpg`. The sources are attached after the page loads, so the video never holds the page up. **To replace it**, drop in new files with the same names, keep them short (about 10 seconds) and small (1 to 2 MB), and update the poster; the paths are in `AD_VIDEO`. To make the MP4 from frames or another video, use the local ffmpeg (`npm install` once, then `node_modules/ffmpeg-static/ffmpeg.exe ... -c:v libx264 -profile:v main -crf 27 -pix_fmt yuv420p -movflags +faststart -an assets/ad/island.mp4`). It only plays while the ad or billboard can be seen, and holds still with reduced motion. There is never a second live 3D island in the billboard.

## The asteroid diorama

- Once the billboard has zoomed out, visitors can drag sideways to spin the camera a full 360 degrees around the asteroid (`SPIN`). Vertical drags still scroll (the stage uses `touch-action: pan-y` in space), and while spinning, Shigost's gaze ignores the finger. The spin eases home once the journey moves on.
- While spun, the 2D tap areas no longer line up, so 3D tap targets for the snail, Shigost, and the billboard take over (they use `hotAt(..., { when })`).
- The diorama is crafted to look good from every side: a little stone arch, a stepping-stone path, pebbles, glowing crystal clusters, a softly glowing crater pond, hanging stones underneath, and little stones drifting in orbit.

## The EDM nature forest

- The jungle is a festival made entirely of nature, with no electronics, just living light: bioluminescent flowers (`blooms`), glowing mushrooms, and the harp bulbs pulse to a 120 BPM beat, the light shafts sway like stage lights in mint, violet, and rose, and fireflies flicker like strobes on the beat. Playing the vine harp makes the whole forest's glow pulse brighter (`LAND.boost`). With reduced motion nothing pulses or strobes.

## The map edge rule (the berm)

- The edge of the world must never be visible, from any camera angle, in any chapter (including the 360 spin). Use the “Disneyland berm” approach: distant dunes, hills, mountains, and haze that blend into the sky.
- The sky is a dome (`skyQ`) that follows the camera and colors by the direction you look, with the haze color at and below the horizon; fog uses the same color, so distant land melts into it. Stars and nebulae live on the dome, all the way around (no flat backdrop planes).
- The land settles onto a hazy plain that runs to the horizon; the dunes have a berm of big distant dunes behind them that sinks under the sea past the coast; the beach runs past the edge of view. The land's ground only shows once the fall's haze has faded in, so it never appears as a slab seen from space.
- Under water the haze does most of the work: fog and the sky dome share the water's color, so the floor, ridges, and big rock silhouettes behind the reef melt into it. Nothing breaks the surface (rocks and kelp are kept under it), a plain sea floor runs under the open sea beside the beach, and past the drop-off pillars rise from the dark blue deep with faint glowing specks.
- When building a new chapter, check the edges from every camera angle it uses (and from high above), and add berms or haze where the world could end.

## Characters and interactions

- **Shigost**: see “Who Shigost is” above. In space she is the 3D model from Vibe Booth: she holds the portal gun and waves when idle, and tapping her fires the gun, eases the camera out, opens the portal, and shows the Space Explorer concept card. She jumps with her arms up, slips out of her hoodie as it becomes the balloon, and hangs from its sleeves in her spirit body. The same 3D model carries her through every chapter: she lands, walks, hops, rests, runs out of the jungle, and leaps into the dunes. The 2D Shigost (separate SVG arm layers, stepping sneakers, idle loops) is only the fallback. The small `#gostSym` version is used in cards, About, and the billboard DJ.
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
- **On the reef**: the **coral xylophone** (seven coral bars on coral rails; tap or drag across), the **glowing anemones** (lean toward a finger or the mouse and chime when touched), a **sea turtle** gliding slowly past on a long loop (a tap sends it into a happy barrel roll), a **little octopus** that peeks out of its coral nook now and then and pops out waving when tapped, **schools of reef fish** (tap the one by the xylophone and it scatters), and two **Womps in bubble helmets**. All white spirits with matte eyes.

## What the reef adapted from Vibe Booth

Read from the public vibe-booth repo (`app.js`), never copied wholesale, and redrawn in the site's matte, wompified style with every animal a white spirit: the depth tint and caustics (`applyUnderwater`, here `underwater()`), the light shafts and rising bubbles, the underside of the water surface (`makeWaterSurface`, here in the sea's shader), and the coral and critter shapes (`coralGeos`, `critterGeos`, and `FISH`, here brain, branching, tube, pom, and fan corals, anemones, and two fish shapes). Vibe Booth's colorful fish and real-world species are not used.

## Design previews

- `preview/parachute.html` compares three ways her hoodie could become the parachute, side by side in real 3D with her model and the fall's sky and lighting: (1) the hoodie flies off (built into the journey), (2) only the hood inflates, and (3) the hem flips up (built into the journey as the flared hem for short drops). Each one can be orbited, seen from the front, the side, and three-quarters behind, and played (pop open and land).
- Option 2 was rebuilt for a fair comparison: the hood lifts up off her shoulders (rather than out of the top of her head) into a big balloon hood, snug around her head low down with its teardrop face opening around her face, billowing into a dome above with the hood's seam over the top, and her drawstrings run from the opening to her hands as the cords. It is **preview only**, not in the journey.
- Previews are unlinked and marked `noindex`. Their stand-in bodies are separate from the journey's spirit body.

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
- World landmarks: asteroid near y 0, hills ground `GROUND` at y 15800, jungle floor `JG` at y 15900, jungle spans x 4250 to 12500, the beach ends near x 30200, the reef runs to its drop-off at x 42700 (`DROP_X`). New chapters continue to the right.
- To add a chapter: extend the scroll length (`#journey` height), add Shigost and camera keyframes after the jungle, add a `CHAPTERS` entry, mark its dot as built in `#rail`, and add its scene objects.

## Performance rules (the iPhone crash)

Mobile Safari ran out of graphics memory and reloaded when the world was built from huge layers. Keep it from coming back:

- World units are drawn at `U` = 0.2 CSS px (`--u` in CSS). **No element may be larger than about 2000 CSS px** in either direction; split anything bigger into tiles. Any CSS px value inside the world must be scaled (`calc(var(--u) * N)` or a percentage).
- Every object belongs to a **chapter group**. `cull()` sets far chapters and far objects to `display: none` each frame. New chapters must call `chapterGroup()` first.
- Touch devices get the `lite` class: no full-screen blend modes, backdrop blur, CSS filters, or sway animations inside big layers, and the star canvas is capped at 1.5x. Don’t add `filter`, `mix-blend-mode`, `backdrop-filter`, or `will-change` to world objects.
- The stage uses `lvh` and the camera frames to `svh`, so the iOS address bar never causes jumps.
- **Test on an iPhone 14 in Safari**: scroll from the top to the newest chapter and back up, three times in a row, with no crash and smooth motion. Before that, a Playwright pass with WebKit and iPhone 14 emulation at every size below is a good first check.

## The 2D cartoon Shigost

- The 2D Shigost (the game cards, the About section, the billboard art, and the 2D fallback; `hoodie()` and `#gostSym`) matches her real design: the long oversized white hoodie to her knees with the hood up, the downward teardrop face opening, big matte black eyes (no highlights), drawstrings, long sleeves over small hands, and chunky white high-tops. Soft lavender lines (`LINE`), never bold outlines, and never on a yellow background.

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
- The crash test runs from the top to the end of the reef and back, three times.
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
- Build the **deep ocean** chapter next (3D), continuing down past the reef's drop-off, with darker blues and glowing creatures. Her hoodie may need a new trick there.
- A **swim** clip for her library, to replace the procedural glide (see “Swimming”).
- Write the **lore** (names and descriptions) in `LORE`, including real names for the Womps.
- Build the Womps out properly and swap them in (see “Womps”), and drop creature models into the space slots (`SPACE_SLOTS`).
- **Accounts and a public leaderboard** built on the journal data, alongside the painting studio.
- **Painting studio** (next round): the painter's canvas (`EASEL`) becomes the door. Visitors tap it, the camera zooms into the canvas (add a camera stop framing it, the way the harp close-up works), they paint, and they submit to a public gallery with voting and a leaderboard. That needs a backend for storage, moderation, and spam protection, so plan it with Alyssa first.
- Push the private **shigost-assets** repo to GitHub (it's committed locally; see its README).
- After the domain transfer: point recklyss.com at GitHub Pages and set up email forwarding for info@recklyss.com.
- About section copy is a draft.

## Working with Alyssa

- She’s a designer who ships and likes clear, step-by-step guidance for anything technical.
- In replies, use Oxford commas and never use em dashes.
- Avoid promising dates on the site. Use statuses like “in production” or “coming soon” instead.
