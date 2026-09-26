# Procedurality-3D

An open-universe observatory that runs entirely in the browser. You don't pilot a ship or play a character. You drift through an infinite, seeded universe and watch it: stars, planets, moons, climates, rivers, alien ecosystems. The universe keeps running whether you're watching or not. Now in 3D.

**Play:** open `index.html` in any modern browser. That's it — one self-contained file, no build step, no server, no dependencies, no network access. Works from `file://`, on desktop and on phones/tablets.

---

## What's in the universe

| Scale | What you see | What's generated |
|---|---|---|
| **Galaxy** | An endless field of stars streamed in 64-unit sectors, cosmic-web density filaments, nebulae | Star class (O B A F G K M, white dwarfs, red giants, pulsars, black holes), temperature, luminosity, mass, radius, age, names |
| **System** | Live orbits, moons, rings, asteroid belts, comets, the habitable zone | Orbital spacing, planet class (rocky / gas giant / ice giant), moons, belts |
| **Planet** | A rotating globe with clouds, atmosphere glow, ocean glint, night-side bioluminescence, lava glow, rings, orbiting moons | Temperature from star + orbit + greenhouse, atmosphere & gases, liquids (water, lava, acid, methane), 15 world types, 22 biomes, resources, surface features, life |
| **Surface** | An isometric pixel-art landscape with day/night, weather and wildlife | Terraced terrain, oceans, rivers with waterfalls, lakes, frozen seas, lava fields, vegetation, ruins, monoliths, arches, geysers, fossils, nests, mineral deposits, creatures |

### Creatures & genetics
* **9 body-plan families** — quadrupeds, bipeds, hexapods, octopods, serpents, avians, aquatic swimmers, gastropods and floating aerostats — each built from instanced primitives and animated procedurally (walk cycles, slithering along a trail, flapping, swimming, hopping, pulsing).
* **45-gene genome** covering anatomy (size, limbs, neck, snout, jaws, tails & tail ornaments, spines, horns, antlers, ears, crests, fins, wings, eyes, armor, fur, segmentation), coloration (hues, saturation, pattern type & scale, bioluminescence) and behavior (speed, aggression, sociality, perception, fertility, longevity, nocturnality, metabolism, tolerances, diet).
* **Environmental adaptation** — gravity shapes limbs, climate shapes coats and ears, dim stars enlarge eyes, dense air favors fliers and aerostats, biomes drive camouflage or warning colors. Each species lists its adaptations and why.
* **Autonomous ecosystems** — agents graze, hunt, flee predators, drink, herd, sleep through the planet's real night (or day, if nocturnal), court and breed. Offspring inherit a **crossover of both parents' genomes plus mutation**; the inspector's *Offspring* tab previews possible children, like a breeding chart.
* **Evolution over universal time** — every niche slot runs a lineage of eras. Each era the genome mutates into a new species; lineages eventually go extinct and new ones arise. This is a pure function of time, so it happens whether or not you are watching. Population cycles follow predator–prey dynamics.

### The autonomous clock
Universal time is derived from the real-world clock plus a persisted offset. Orbits, planetary rotation (day/night), weather, population cycles and evolution are all functions of that clock — close the tab, come back tomorrow, and planets have moved and saved worlds have evolved. You can speed time up (×10, ×100, ×1000) or freeze observation.

## Controls

| | Desktop | Touch |
|---|---|---|
| Pan | drag · WASD / arrows | one-finger drag |
| Zoom | scroll · + / − | pinch |
| Rotate / tilt | right-drag · shift-drag · Q/E · R/F | two-finger twist / two-finger vertical drag |
| Inspect | click | tap |
| Enter / descend / follow | double-click · Enter | double-tap |
| Back | Esc · ← button | ← button |
| Time | Space (freeze) · 1–4 speeds | clock buttons |
| Tools | `/` scanner · `B` saved · `G` seeds · `P` autopilot · `H` hide UI · `?` help | ☰ menu |

In the planet view, drag spins the globe and a tap drops a landing pin that rotates with the planet.

## Seeds & sharing

Everything is regenerated exactly from seeds — nothing is stored except your bookmarks.

* `ORIGIN:12,-4:3` — universe `ORIGIN`, sector (12, −4), star #3
* `ORIGIN:12,-4:3:2` — …planet #2
* `ORIGIN:12,-4:3:2:0` — …its first moon
* `ORIGIN:12,-4:3:2@14.210,-33.050` — a surface site at latitude/longitude
* `SEED~emerald dawn` — any words create a *pocket system* outside the galaxy map
* `U:ORIGIN@1200,-800` — a galactic position

Codes appear in the URL hash, so links are shareable. Change the **universe seed** on the title screen or in *Seeds & codes* to get an entirely different infinite universe.

## Tools
* **Survey scanner** — searches outward from the current sector for worlds matching type, star class, life, species count, moons and rings.
* **Random world** — warps to a random world (usually one with life).
* **Saved** — bookmarked stars/planets/surface sites and an automatic catalogue of every species you have observed, with portraits. Export/import as JSON.
* **Procedural generation details** — for any planet: the seed-hash chain, orbital/climate derivation, terrain noise parameters, equirectangular elevation / temperature / moisture / biome maps, biome distribution and niche slots.
* **Autopilot** — the observer drifts on its own: slow orbits, and on surfaces the camera follows a random creature, switching every ~25 s.
* Settings: pixel size (auto or 1–6×), quality, outlines, retro color quantization, vignette, FPS.

## How it works

Everything lives in `index.html`, split into modules (one `<script>` each):

| Module | Responsibility |
|---|---|
| **Core** | column-major matrix math, matrix stack, string/integer hashing, mulberry32 PRNG streams, seeded 2D/3D simplex noise (fBm, ridged, domain warp), color utilities, syllable name generator |
| **Generation** | universe sectors & density field, star records, systems (Titius–Bode-like spacing, habitable zone, frost line), planet physics & classification, biome classifier, palettes, flora profiles, resources, seed codes |
| **Genetics** | gene table, families, phenotype expression, mutation & crossover, species factory, environmental adaptation, deterministic lineages/eras, food web, population dynamics |
| **Surface** | terrain chunks (planet field + planet-anchored local 3D noise, terraces, rivers, lakes), water meshes, vegetation & structure mesh baking |
| **GFX / Render** | WebGL2 helpers, instancing, CPU mesh builder, GLSL shaders (toon lighting with Bayer dithering, water/lava/ice, globe, clouds, gas bands, rings, stars, nebulae), low-resolution MRT target and a post pass that upscales with nearest filtering and draws pixel outlines from depth + normals |
| **Life** | procedural rigs for all nine families, and the agent simulation |
| **Views** | galaxy, system, planet and surface views, weather & particles |
| **UI** | persistence (localStorage), universal clock, panels / bottom sheet, modals, portraits (offscreen sprite renders), planet thumbnails, unified pointer/touch/keyboard input |
| **App** | navigation, dissolve transitions, URL hash, main loop, splash |

### Rendering style
The scene is drawn into a low-resolution multi-render-target framebuffer (color, view normals + outline strength, depth), then upscaled by an integer factor with nearest sampling. The post pass detects silhouettes (depth discontinuities) and creases (normal changes) per low-res pixel and darkens them, giving 1-pixel sprite outlines. Lighting is quantized into bands with ordered (Bayer) dithering; sky, nebulae, clouds and rings use dithered alpha. The surface uses an orthographic isometric camera.

### Performance
Terrain chunks and globe meshes are generated on the CPU with time-sliced budgets; planet-scale fields are sampled on a coarse grid and interpolated; vegetation and structures are baked into one mesh per chunk; creatures are drawn with four instanced draw calls; off-screen chunks and creatures are culled. The *Low* quality preset (default on phones) reduces globe resolution, chunk budget and creature caps.

## Browser support
Requires WebGL 2 — current Chrome, Edge, Firefox, and Safari 15+ (iOS/iPadOS included).
