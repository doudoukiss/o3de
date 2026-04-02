# 90-Day Roadmap

This roadmap turns the study set in `docs/study/` into a paced three-month learning plan. The goal is not speed-reading the repo. The goal is building enough understanding to make sound decisions for your own future MMORPG engine.

Companions:

- [Main tutorial](./o3de-engine-study-tutorial.md)
- [Repo map and reading order](./repo-map-and-reading-order.md)
- [Staged labs](./staged-labs.md)
- [MMORPG engine extraction](./mmorpg-engine-extraction.md)

## How To Use This Roadmap

- Spend four to eight focused hours per week if possible.
- Keep a running engineering notebook the whole time.
- End each week by writing what you would keep, simplify, replace, or move outside the engine.
- If a week runs long, do not rush. Depth matters more than staying on a calendar.

## Phase 1: Orientation And Foundations

### Weeks 1-2

Focus:

- top-level repo shape
- engine composition
- build and manifest files

Read:

- [Main tutorial, Chapter 1](./o3de-engine-study-tutorial.md#1-o3de-as-a-codebase-and-product)
- [Repo map and reading order](./repo-map-and-reading-order.md)

Do:

- [Lab 1](./staged-labs.md#lab-1-trace-engine-bootstrapping)

Outcome:

You can explain how O3DE is assembled and where the major product areas live.

### Weeks 3-4

Focus:

- `AzCore`
- `AzFramework`
- `AzGameFramework`
- tests as documentation

Read:

- [Main tutorial, Chapter 2](./o3de-engine-study-tutorial.md#2-core-runtime-foundations-azcore-azframework-azgameframework)
- [Glossary and concepts](./glossary-and-concepts.md)

Do:

- [Lab 2](./staged-labs.md#lab-2-trace-a-core-abstraction-through-azcore)

Outcome:

You understand the difference between core engine foundations and higher-level runtime systems.

## Phase 2: Tools, Assets, And Rendering

### Weeks 5-6

Focus:

- `AzToolsFramework`
- `Code/Editor`
- `Code/Tools/ProjectManager`
- `Code/Tools/SceneAPI`

Read:

- [Main tutorial, Chapter 3](./o3de-engine-study-tutorial.md#3-editor-and-tools-architecture)

Do:

- Write a note on which authoring features your own engine actually needs in v1.

Outcome:

You understand that a serious engine is also a tool platform.

### Weeks 7-8

Focus:

- Asset Processor
- builder model
- source asset versus runtime product

Read:

- [Main tutorial, Chapter 4](./o3de-engine-study-tutorial.md#4-asset-pipeline-asset-processor-builders-scene-api-runtime-asset-flow)

Do:

- [Lab 3](./staged-labs.md#lab-3-trace-an-asset-from-source-to-runtime-product)

Outcome:

You can explain the asset pipeline as an engine subsystem, not just as a build script.

### Weeks 9-10

Focus:

- Atom
- RHI and RPI
- feature layering

Read:

- [Main tutorial, Chapter 5](./o3de-engine-study-tutorial.md#5-rendering-architecture-atom-rhi-rpi-feature-layers)

Do:

- [Lab 4](./staged-labs.md#lab-4-trace-a-render-path-through-atom)

Outcome:

You understand how O3DE separates backend rendering concerns from engine-facing rendering systems.

## Phase 3: World Systems, Networking, And Extraction

### Weeks 11-12

Focus:

- prefabs and spawnables
- physics
- terrain
- navigation
- animation
- `AzNetworking`
- `Gems/Multiplayer`
- client/server/unified patterns
- custom engine scope
- engine versus backend service boundary

Read:

- [Main tutorial, Chapter 6](./o3de-engine-study-tutorial.md#6-world-and-simulation-systems-entities-prefabs-spawnables-physics-terrain-navigation-animation)
- [Main tutorial, Chapter 7](./o3de-engine-study-tutorial.md#7-networking-and-gameplay-replication-aznetworking-multiplayer-clientserverunified-split)
- [Main tutorial, Chapter 8](./o3de-engine-study-tutorial.md#8-what-to-learn-from-o3de-for-your-own-mmorpg-engine)
- [MMORPG engine extraction](./mmorpg-engine-extraction.md)

Do:

- Compare authoring-time versus runtime representations in your notes.
- [Lab 5](./staged-labs.md#lab-5-trace-a-replicated-gameplay-component)
- [Lab 6](./staged-labs.md#lab-6-write-your-mmorpg-engine-cut-list)

Outcome:

You can describe how O3DE composes a simulated world, distinguish transport from replication and MMO service concerns, and end the roadmap with a first architecture boundary for your own engine.

## Optional Parallel Track: Hands-On Setup

Do this only when the reading flow feels stable:

- follow the top-level `README.md` build steps
- bootstrap Python if needed with `python\\get_python.bat`
- configure a build tree with CMake
- register the engine with `scripts\\o3de.bat register --this-engine`
- create a small project or Gem from a template

The right time for hands-on setup is when it reinforces your mental model, not before.

## Final Deliverables To Produce For Yourself

At the end of 90 days, aim to have:

- a repo map in your own words
- subsystem notes for runtime, assets, rendering, world systems, and networking
- an MMORPG engine cut list
- a v1 engine boundary document
- a list of features you explicitly will not build in the first iteration

If you produce those five artifacts, the study plan worked.
