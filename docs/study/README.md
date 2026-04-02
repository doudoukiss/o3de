# O3DE Study Curriculum

This folder is a guided study set for learning the O3DE repository in a way that is directly useful for building your own future 3D engine for an MMORPG.

The material is intentionally split into one linear tutorial plus a few companion references:

- [Main tutorial](./o3de-engine-study-tutorial.md): the primary path through the engine.
- [Repo map and reading order](./repo-map-and-reading-order.md): a code-reading companion for navigating the repository.
- [Glossary and concepts](./glossary-and-concepts.md): O3DE-specific terms that appear throughout the repo.
- [Staged labs](./staged-labs.md): reading-first exercises, with later optional hands-on work.
- [MMORPG engine extraction](./mmorpg-engine-extraction.md): lessons to keep, simplify, replace, or move outside the engine.
- [90-day roadmap](./90-day-roadmap.md): a paced study plan that turns the documents into a concrete learning program.

## Who This Is For

This study set assumes:

- You are already a capable programmer.
- You are willing to read C++, CMake, and engine configuration files.
- You want to understand O3DE deeply enough to make informed architecture decisions for your own engine.
- You do not want a build-first course that blocks on setup before you understand the code.

## Reading Order

If you want the best default path, use this order:

1. [Main tutorial](./o3de-engine-study-tutorial.md)
2. [Glossary and concepts](./glossary-and-concepts.md)
3. [Repo map and reading order](./repo-map-and-reading-order.md)
4. [Staged labs](./staged-labs.md)
5. [MMORPG engine extraction](./mmorpg-engine-extraction.md)
6. [90-day roadmap](./90-day-roadmap.md)

If you only have one evening, read the main tutorial first, then jump to the MMORPG extraction document.

## What You Will Learn

By the end of this study set, you should be able to answer:

- How O3DE is assembled from framework libraries, tools, and Gems.
- Where rendering, asset processing, editor systems, physics, and multiplayer actually live in this repo.
- How O3DE separates low-level engine infrastructure from higher-level feature systems.
- Which ideas are valuable for your own engine, and which ones are too heavy or too O3DE-specific to copy directly.
- Which MMO problems belong in the engine and which belong in backend services.

## Top-Level Repo Orientation

The first useful mental model is that O3DE is not just "an engine runtime." It is a source engine, editor, asset pipeline, toolchain, template library, and project ecosystem in one repository.

| Path | What It Primarily Contains | Why You Care |
| --- | --- | --- |
| `CMakeLists.txt` | Root build entrypoint | Shows how the whole repo is assembled. |
| `engine.json` | Engine metadata and built-in external subdirectories | Shows which Gems, templates, and projects ship with the engine. |
| `Code/Framework` | Core reusable engine libraries | This is the best starting point for engine architecture. |
| `Code/Editor` | Editor application code | Useful for learning authoring workflows and engine/editor boundaries. |
| `Code/Tools` | Asset Processor, Project Manager, Scene API, test tooling | Critical for understanding the production pipeline around the runtime. |
| `Code/LauncherUnified` | Runtime launcher entrypoints | Useful for understanding how projects boot into game, server, or unified targets. |
| `Gems` | Feature packages such as Atom, Multiplayer, Terrain, PhysX, RecastNavigation, EMotionFX | Most visible engine systems live here. |
| `Templates` | Project and Gem templates | Helpful for understanding supported extension patterns. |
| `Assets` | Engine-provided assets | Useful when you want to trace data-driven systems into runtime. |
| `AutomatedTesting` | Sample project and test content | Helpful later for real usage examples. |
| `Code/Legacy` | Older code carried forward from earlier engine history | Read later, not first. |

## How To Use This Study Set

- Keep the repo open while reading.
- Treat tests as part of the documentation.
- Read directories first, then files, then classes.
- Do not try to understand every Gem on the first pass.
- Write your own notes after every chapter or lab, especially the design lessons you would keep for your own engine.

## Setup Caveat

This curriculum is intentionally reading-first. In this checkout, the `scripts/o3de.py` CLI complained about a missing O3DE Python virtual environment until Python bootstrap was set up. That is normal enough that the labs do not assume the CLI is ready on day one.

When you do want CLI-based work later:

- Prefer the build and setup instructions from the top-level `README.md`.
- If `scripts/o3de.bat` or `scripts/o3de.py` reports a missing Python venv, bootstrap it with `python\\get_python.bat` first.

## Suggested Outcome

The best result is not "I know every O3DE directory." The best result is:

- You know how to read a large engine codebase without getting lost.
- You can distinguish engine concerns from game concerns from MMO service concerns.
- You can define a realistic v1 architecture for your own engine instead of copying a giant engine wholesale.

See also: [Main tutorial](./o3de-engine-study-tutorial.md), [Repo map](./repo-map-and-reading-order.md), [MMORPG extraction](./mmorpg-engine-extraction.md)
