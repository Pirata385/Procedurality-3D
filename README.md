# Procedurality-3D

An open-universe observatory that runs entirely in the browser. You don't pilot a ship or play a character. You drift through an infinite, seeded universe and watch it: stars, planets, moons, climates, rivers, alien ecosystems — and the civilizations that rise, trade, war and spread between the stars. The universe keeps running whether you're watching or not. Now in 3D.

**Play:** open `index.html` in any modern browser. The whole game is one file — no build step, no server, no dependencies. Music and sound effects are streamed from the `audio/` folder next to it (keep the two together); without that folder the game still runs, just silently. Works from `file://` and on the web, on desktop and on phones/tablets.

---

## What's in the universe

| Scale | What you see | What's generated |
|---|---|---|
| **Galaxy** | An endless field of stars streamed in 64-unit sectors, cosmic-web density filaments, nebulae | Star class (O B A F G K M, white dwarfs, red giants, pulsars, black holes), temperature, luminosity, mass, radius, age, names |
| **System** | Live orbits, moons, rings, asteroid belts, comets, the habitable zone | Orbital spacing, planet class (rocky / gas giant / ice giant), moons, belts |
| **Planet** | A rotating globe with clouds, atmosphere glow, ocean glint, night-side bioluminescence, lava glow, rings, orbiting moons | Temperature from star + orbit + greenhouse, atmosphere & gases, liquids (water, lava, acid, methane), 15 world types, 22 biomes, resources, surface features, life |
| **Surface** | An isometric pixel-art landscape with day/night, weather, wildlife and cities | Terraced terrain, oceans, rivers with waterfalls, lakes, frozen seas, lava fields, vegetation, ruins, monoliths, arches, geysers, fossils, nests, mineral deposits, creatures, settlements, citizens, vehicles, spacecraft |
| **Gas giants** | No ground at all: you hang inside a bottomless atmosphere | Layered cloud decks at several depths with haze, wind-sheared streaks and bands, drifting cloud formations, zonal jets that alternate with latitude, squalls and hurricanes (eye, eyewall, spiral rain bands, lightning, rain), the planet's great storm when you are under it |

### Creatures & genetics
* **9 body-plan families** — quadrupeds, bipeds, hexapods, octopods, serpents, avians, aquatic swimmers, gastropods and floating aerostats — each built from instanced primitives and animated procedurally (walk cycles, slithering along a trail, flapping, swimming, hopping, pulsing).
* **45-gene genome** covering anatomy (size, limbs, neck, snout, jaws, tails & tail ornaments, spines, horns, antlers, ears, crests, fins, wings, eyes, armor, fur, segmentation), coloration (hues, saturation, pattern type & scale, bioluminescence) and behavior (speed, aggression, sociality, perception, fertility, longevity, nocturnality, metabolism, tolerances, diet).
* **Environmental adaptation** — gravity shapes limbs, climate shapes coats and ears, dim stars enlarge eyes, dense air favors fliers and aerostats, biomes drive camouflage or warning colors. Each species lists its adaptations and why.
* **Autonomous ecosystems** — agents graze, hunt, flee predators, drink, herd, sleep through the planet's real night (or day, if nocturnal), court and breed. Offspring inherit a **crossover of both parents' genomes plus mutation**; the inspector's *Offspring* tab previews possible children, like a breeding chart.
* **Persistent wildlife** — creatures are never deleted for being off screen. Every patch of ground is populated once, the first time it is loaded; afterwards its creatures keep their exact state. Only creatures inside the rendered area are simulated — the rest are frozen in place and pick up exactly where they left off when you look again. Idle wandering stays inside the rendered area, and newcomers wander in (out of sight) only to replace creatures that died, so the view never drains or overfills. Civilizations, economies, wars and colonization are never affected by this: they run on universal time everywhere.
* **Aerostats only on gas giants** — nothing can walk, swim or land in a bottomless atmosphere, so gas giants host only floating aerostats. They ride slowly up and down between the cloud layers, drift with the jet stream, get caught in storm vortices, and when they die they sink into the depths.
* **Terrain-aware navigation** — every creature knows where it may go (walkers stay out of deep water, swimmers out of shallows, land and ice). Look-ahead probes steer smoothly around shorelines, grid A* plans routes around lakes and bays, collisions slide along boundaries, and stuck or circling creatures are detected and recover with a new reachable goal — no spinning at the water's edge.
* **Evolution over universal time** — every niche slot runs a lineage of eras. Each era the genome mutates into a new species; lineages eventually go extinct and new ones arise. This is a pure function of time, so it happens whether or not you are watching — and because it is deterministic, each species page shows its full **lineage timeline** (ancestor portraits) and forecasts its next descendant or its extinction. Population cycles follow predator–prey dynamics.

### Civilizations
On some living worlds a species becomes **sapient** and founds several independent **tribes**. Each people carries a hidden progression value (XP) that grows with population, discoveries, successful activities, conflicts, trade, exploration and technology. It is never shown — you only see its effects as a civilization advances through four stages:

1. **Tribal** — tribes coexist, barter, form alliances, stay neutral or fight; wars end in peace, conquest or extermination, and allied tribes may unite.
2. **Nation** — tribes become kingdoms, republics, theocracies or leagues with diplomacy, warfare, alliances, neutrality and **international trade**.
3. **System colonization** — spacefaring peoples settle the planets and moons of their home system (never gas giants): **domed cities** on uninhabitable worlds, **open cities** on habitable ones, with supply and trade routes between colonies.
4. **Intergalactic** — they **terraform** domed colonies into new habitable worlds, travel to nearby star systems, open **interstellar trade routes**, form alliances, wage wars, conquer holdings and even exterminate rivals — including less advanced peoples they discover.

**Culture is procedural and specific to each people**: values (warlike, mercantile, devout, open…), a color-harmony palette, architecture (domed, gabled, stepped, spired, organic, monolithic, crystalline, pavilion), city layout (grid, radial, organic, linear, ringed, terraced), building material, clothing and headgear, melee and ranged weapons that evolve with each stage, vehicles, spacecraft hulls, technology aesthetic, a 7×7 heraldic emblem and a culture-specific phonology for every name.

Beyond the stage machine every people **researches** named technologies step by step, builds **great works** (libraries, cathedrals, aqueducts, observatories, space elevators, stellar gates…) that take hours to finish, **founds settlements** that can later be captured or razed, **explores** its world (mountain ranges, seas, poles, circumnavigation), launches **probes** to the other worlds of its system, sends **colony ships** and interstellar **colony fleets** that take real time to arrive, **trades named goods** (grain and furs, spices and silk, fuel cells and alloys, antimatter…), passes population milestones, and fights **named battles** at real places.

Where to see it — everything below happens in real time, on the universal clock:
* **Surface** — land on a settlement to watch it live:
  * **Construction** — cities grow house by house after a settlement is founded or a new age begins; building sites have foundations, rising walls, scaffolding, stacked materials and swinging cranes (assembly drones for starfaring peoples), and existing houses are periodically rebuilt. Finished buildings join the city; great works rise on reserved plots around the plaza.
  * **Farming & production** — crops sprout, ripen and are harvested row by row; farmers tend and harvest the fields and carry sacks to the granary, whose stock rises and falls with the harvest. Chimneys smoke, windmills turn, spaceport vents steam.
  * **Trade & transport** — market stalls with merchants, carts carrying cargo through the streets, caravans on roads between cities (foreign traders in their own colours), shuttles loading crates at landing pads, ships overhead.
  * **Research** — every city has a house of learning (shrine, observatory, laboratory or research spire) with moving instruments and scholars; a pillar of light rises from it when its people make a discovery.
  * **Exploration** — expeditions set out from the city into the wilds and plant their people's flag; flags of past expeditions stay where they were planted.
  * **War** — battles recorded by the history engine at a settlement are fought there when you watch: an army musters on dry ground and marches in, the city's warriors and militia defend it, townsfolk flee, archers and gunners keep their distance and shoot visible projectiles (arrows, bolts, rail slugs, energy bolts), buildings burn. Spacefaring enemies send fighters that duel over the city, trade bolts and are shot down. Neighbours at war also skirmish.
  * **Colonies & terraforming** — colony ships and probes lift off from spaceports (and land at colonies); terraforming processors around colonies breathe out new atmosphere while the sky slowly changes colour.
  * **Growth** — when the civilization changes (a new settlement nearby, a new age, a conquest, a ruin) the cities around you are re-planned and rebuilt on the spot, and the log tells you what happened.
* **Planet** — the *Civilization* tab, city lights sprawling across the night side, trade and supply routes between settlements with cargo moving along them, battles flaring at contested cities (and in orbit), colony ships and probes rising from their spaceports, a thickening veil over a world being terraformed, ships and orbital stations.
* **System** — freighters and supply ships flying the routes between worlds, warships massing on routes of war, colony ships and probes on their way (with wakes), colony fleets leaving for or arriving from other stars, weapons fire around contested worlds, and terraforming progress on each world.
* **Galaxy** — territories, supply/trade/alliance/war routes with ships moving along them, colony fleets crossing interstellar space, and battles flaring at the stars where they are fought.
* **Civilization dossier** — emblem, a portrait of a citizen, stage timeline, population, culture, what the people is doing *now* (current research and great work with progress, ships under way, trade partners and goods), diplomacy, colonies and holdings, and its complete **History**.
* **City panel** — an *Activity* tab with founding date, buildings standing and under construction, the next completion, the state of the fields, what its scholars study, who is in the streets, its great works, trade roads and goods, and the battles fought there.

History is simulated per **galactic region** (4×4 sectors) in 10-minute steps from the start of the region's current **age** (20–48 hours of universal time). It is a pure function of the universe seed and the clock, so it advances while you are away and every observer sees the same chronicle.

**Persistent history** — every civilization keeps its complete record for the whole age: discoveries and research breakthroughs, wars, battles, alliances, treaties, settlements founded, captured or razed, colonies and expansion, great works begun and completed, trade routes and trade milestones, exploration, terraforming, population milestones, new ages, disasters. Open a dossier and read it in the *History* section, filtered by category (discoveries, wars & battles, diplomacy, settlements & colonies, great works, trade, exploration, terraforming, growth & ages) and paged back to the very first entry. Because history is deterministic it is persistent without being stored: it is exactly the same after a reload, on another device or for another observer. Under heavy time acceleration the live log shows the latest events and counts the rest.

### Sound
* **Music** — *space themes* play in the galaxy and system views, *planet themes* while you orbit a world or explore its surface. Tracks don't loop back to back: after each piece there is a quiet break (short, normal or long — your choice), the same track never plays twice in a row, and moving between space and a planet fades the current piece out before the matching theme begins.
* **Rain ambience** — a seamless cross-faded loop that follows the local rain intensity on the surface, a little softer when zoomed out, and fades away when the rain stops or time is frozen.
* **Creature calls** — each body plan has its own voice: quadrupeds by niche (herbivore, megaherbivore, forager, predator, apex predator), bipeds, hexapods, octopods, serpents, avians, gastropods and aerostats (a species always keeps the same variant; aquatic swimmers are silent). Creatures call when they **attack** (charging prey, striking, fighting), when they **try to escape** a predator (a higher-pitched alarm), and when you **click** them. Bigger bodies sound deeper, juveniles higher, and every individual has its own pitch. Calls are panned by screen position, fade with distance and zoom, and are rate-limited so herds and fast time stay pleasant. Sapient citizens use their species' voice.
* Interface clicks, a master/music/creature/ambience mixer, music frequency and mute live in **Settings**; `M` toggles sound. Every file was loudness-measured so all sounds sit at balanced levels, with leading silence trimmed.
* Over `http(s)` (e.g. GitHub Pages) audio runs through Web Audio (stereo panning, gain, a limiter, iOS-safe unlocking on the first tap); from `file://` it falls back to plain media elements.

### The autonomous clock
Every universe has its **own universal cycle counter**, which starts at exactly **Cycle 0** when that universe is first generated. It is derived from the real-world clock plus a persisted per-universe offset, so switching universes never carries time over from another universe or save. Orbits, planetary rotation (day/night), weather, population cycles, evolution and history are all functions of that clock — close the tab, come back tomorrow, and planets have moved and saved worlds have evolved. You can speed time up (×10, ×100, ×1000) or freeze observation (freezing is exact: no drift). *Settings → Reset universe clock* sets the current universe back to Cycle 0 and rebuilds everything from that moment; other universes keep their own time. Saves from earlier versions keep their timeline until you reset it.

**Time acceleration without desync** — creatures, citizens, projectiles and city activity are simulated in **fixed time steps locked to the universal clock** (an accumulator: 1/30 s steps at ×1, 1/15 s at ×10, ¼ s at ×100, 1 s at ×1000), with render interpolation between steps. Every step is the same size whatever the frame rate, so frame slicing never changes the outcome, and movement, behavior, reproduction, farming, construction, exploration and combat all advance in proportion to universal time at every speed. Swept movement and swept contact tests keep large steps from skipping over water or through prey. Only if a device cannot keep up does the simulation temporarily take coarser steps until it catches up. Vehicles, ships, crops, construction and storms are pure functions of time and cannot fall behind.

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
| Tools | `/` scanner · `B` saved · `G` seeds · `P` autopilot · `M` sound · `H` hide UI · `?` help | ☰ menu |

In the planet view, drag spins the globe and a tap drops a landing pin that rotates with the planet.

## Seeds & sharing

Everything is regenerated exactly from seeds — nothing is stored except your bookmarks.

* `ORIGIN:12,-4:3` — universe `ORIGIN`, sector (12, −4), star #3
* `ORIGIN:12,-4:3:2` — …planet #2
* `ORIGIN:12,-4:3:2:0` — …its first moon
* `ORIGIN:12,-4:3:2@14.210,-33.050` — a surface site at latitude/longitude
* `SEED~emerald dawn` — any words create a *pocket system* outside the galaxy map
* `U:ORIGIN@1200,-800` — a galactic position
* `ORIGIN:12,-4:3:2$629.1` — a civilization: its homeworld code, the age, and the tribe index

Codes appear in the URL hash, so links are shareable. Change the **universe seed** on the title screen or in *Seeds & codes* to get an entirely different infinite universe.

## Tools
* **Survey scanner** — searches outward from the current sector for worlds matching type, star class, life, species count, moons, rings and civilizations (by stage, colonies or fallen peoples).
* **Random world** — warps to a random world (usually one with life).
* **Saved** — bookmarked stars/planets/surface sites, saved civilizations, and an automatic catalogue of every species you have observed, with portraits. Export/import as JSON.
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
| **Civilizations** | culture generator (values, palette, architecture, layout, clothing, weapons, vehicles, hulls, emblem, phonology); region/age history engine with hidden XP, stages, diplomacy, war, trade, colonization, terraforming, interstellar expansion, conquest & extermination; settlement geography; terraformed world variants |
| **GFX / Render** | WebGL2 helpers, instancing, CPU mesh builder, GLSL shaders (toon lighting with Bayer dithering, water/lava/ice, globe, clouds, gas bands, rings, stars, nebulae), low-resolution MRT target and a post pass that upscales with nearest filtering and draws pixel outlines from depth + normals |
| **Life** | procedural rigs for all nine families (with clothing, headgear and weapons for sapient peoples), and the agent simulation |
| **Nav** | per-habitat terrain legality, look-ahead steering, grid A* with line-of-sight smoothing, sliding collisions, stuck/circling detection and recovery |
| **Cities** | settlement layouts, terrain levelling and street painting, construction timelines, great works, houses of learning, markets, granaries, roads between cities, buildings baked into a per-chunk city mesh by architecture and stage, domes, pads, walls, monuments; vehicle and spacecraft models |
| **City life** | citizens at work (builders, farmers, scholars, merchants, explorers, warriors), battles with projectiles and militia, air combat, caravans and traffic, crops and harvests, smoke and windmills, discovery beams, flags, launches and landings, terraforming processors |
| **Views** | galaxy, system, planet and surface views (fixed-step simulation, rendered-area activation, living cities that re-bake and re-plan), weather & particles |
| **Gas giants** | bottomless atmosphere: cloud-deck shader with wind flow, storm vortices and lightning, drifting cloud formations, storm schedules, zonal winds |
| **UI** | persistence (localStorage), universal clock, panels / bottom sheet, modals, portraits (offscreen sprite renders), planet thumbnails, unified pointer/touch/keyboard input |
| **Audio** | music scheduler with breaks and theme switching, cross-faded rain loop, creature voices (mapping, pitch, panning, distance, rate limits), UI clicks, mixer settings, Web Audio with media-element fallback |
| **App** | navigation, dissolve transitions, URL hash, main loop, splash |

### Rendering style
The scene is drawn into a low-resolution multi-render-target framebuffer (color, view normals + outline strength, depth), then upscaled by an integer factor with nearest sampling. The post pass detects silhouettes (depth discontinuities) and creases (normal changes) per low-res pixel and darkens them, giving 1-pixel sprite outlines. Lighting is quantized into bands with ordered (Bayer) dithering; sky, nebulae, clouds and rings use dithered alpha. The surface uses an orthographic isometric camera.

### Performance
Terrain chunks and globe meshes are generated on the CPU with time-sliced budgets; planet-scale fields are sampled on a coarse grid and interpolated; vegetation is baked into one mesh per chunk and city structures into a second one that is re-baked (a couple of chunks per frame) as buildings are completed; creatures are drawn with four instanced draw calls; off-screen chunks are culled and off-screen creatures are frozen rather than simulated. The creature simulation uses a spatial hash, a per-step path-planning budget and a CPU budget proportional to the frame time. Civilization regions are built incrementally (time-sliced on the galaxy map) and advanced step by step as the clock moves; roads are painted through a spatial index. The *Low* quality preset (default on phones) reduces globe resolution, chunk budget, creature density and caps and citizen counts.

## Browser support
Requires WebGL 2 — current Chrome, Edge, Firefox, and Safari 15+ (iOS/iPadOS included).
