# Glossary And Concepts

This glossary explains recurring O3DE terms that can slow down first-time readers. Each entry includes a practical definition and a "where to see it" pointer in the repo.

Companions:

- [Main tutorial](./o3de-engine-study-tutorial.md)
- [Repo map and reading order](./repo-map-and-reading-order.md)
- [Staged labs](./staged-labs.md)
- [MMORPG engine extraction](./mmorpg-engine-extraction.md)
- [90-day roadmap](./90-day-roadmap.md)

## Gem

A Gem is an O3DE package boundary for engine or project functionality. Gems can contain code, assets, configuration, editor integration, tests, or some combination of these. In practice, they are one of O3DE's primary extension and modularization units.

Why it matters:

- Many major systems live in Gems, not just optional add-ons.
- Gems are one of the main ways O3DE avoids putting every feature in the framework core.

Where to see it:

- `engine.json`
- `Gems/Multiplayer/gem.json`
- `Gems/Atom/gem.json`

## EBus

EBus is O3DE's event and request bus pattern. It is used heavily for decoupled communication across systems.

Why it matters:

- You will see it in runtime, tools, and feature Gems.
- It expresses engine boundaries, but it can also hide control flow if overused.

Where to see it:

- `Code/Framework/AzCore/AzCore/EBus`
- `Code/Framework/AzCore/Tests/EBus.cpp`
- `Gems/RecastNavigation/Code/Include/RecastNavigation/RecastNavigationBus.h`

## Settings Registry

The Settings Registry is O3DE's structured runtime and build-time configuration system. It is closely tied to generated and static `.setreg` data and is part of how applications discover what modules, Gems, or settings to load.

Why it matters:

- It is part of O3DE's configuration spine.
- It helps decouple configuration data from hardcoded startup logic.

Where to see it:

- `CMakeLists.txt`
- `Registry`
- `Code/Tools/AssetProcessor/testdata`

## Prefab

A prefab is an authored composition unit: a reusable definition of entities and related content created for authoring workflows and reuse.

Why it matters:

- Prefabs tell you how O3DE thinks about authored world structure.
- They are useful for understanding authoring-time composition.

Where to see it:

- `Gems/Prefab/PrefabBuilder`
- `Gems/Prefab/PrefabBuilder/PrefabBuilderComponent.cpp`

## Spawnable

A spawnable is a runtime-oriented representation for instancing content. It is closely related to loading and spawning scene data efficiently at runtime.

Why it matters:

- It marks a useful distinction between authoring representation and runtime representation.
- This distinction becomes increasingly important in streaming-heavy games.

Where to see it:

- `Code/Framework/AzFramework/AzFramework/Spawnable`

## Launcher

A launcher is a runtime application entrypoint built around a particular target role such as game, server, or unified runtime.

Why it matters:

- It shows how projects actually boot.
- It also reveals O3DE's client/server target split for multiplayer-aware applications.

Where to see it:

- `Code/LauncherUnified`
- `Templates/UnifiedMultiplayerGem/Template/README.md`

## Builder

A builder is a tool-side processor that converts source assets into runtime product assets. Builders run within the broader asset pipeline rather than inside the game runtime.

Why it matters:

- Builders are the key to understanding why source content is different from loadable runtime data.
- They are also an important extension point for custom engines.

Where to see it:

- `Code/Tools/AssetProcessor/AssetBuilderSDK/AssetBuilderSDK/AssetBuilderBusses.h`
- `Gems/Atom/Asset/Shader/Code/Source/Editor/ShaderAssetBuilder.cpp`

## RHI

RHI stands for Rendering Hardware Interface. In O3DE, this is the low-level rendering abstraction layer that sits close to graphics APIs and backend-specific implementations.

Why it matters:

- It isolates backend concerns such as DX12, Vulkan, Metal, and Null.
- It is not enough by itself to explain the whole renderer; it is the lower rendering layer.

Where to see it:

- `Gems/Atom/RHI`
- `Gems/Atom/RHI/DX12`
- `Gems/Atom/RHI/Vulkan`

## RPI

RPI stands for Rendering Platform Interface. In O3DE, it is the higher-level rendering layer above RHI that deals with materials, passes, shader resources, models, and engine-facing render systems.

Why it matters:

- It is where rendering becomes engine-usable rather than merely backend-abstract.
- It is a strong example of layering beyond raw API abstraction.

Where to see it:

- `Gems/Atom/RPI`
- `Gems/Atom/RPI/Code/Source/RPI.Public`
- `Gems/Atom/RPI/Code/Tests/Pass`

## Reflection

Reflection is O3DE's ability to describe types, fields, serialization behavior, editing metadata, and scripting exposure in a structured way that the engine and tools can inspect.

Why it matters:

- It underpins serialization, editors, tools, and often scripting or data-driven workflows.
- It is a major reason why engine types can participate in multiple systems without ad hoc glue everywhere.

Where to see it:

- `Code/Framework/AzCore/AzCore/RTTI`
- `Code/Framework/AzCore/Tests/Serialization.cpp`
- `Code/Framework/AzCore/Tests/BehaviorContext.cpp`

## Module

A module is a loadable or statically linked packaging unit that registers engine functionality, component descriptors, and related systems at application startup.

Why it matters:

- Modules are part of how O3DE assembles applications from many subsystems.
- They reveal the startup and registration model of the engine.

Where to see it:

- `Code/Framework/AzNetworking/AzNetworking/AzNetworkingModule.cpp`
- `Code/LauncherUnified/StaticModules.in`
- `Gems/Prefab/PrefabBuilder/PrefabBuilderModule.cpp`

## A Useful Mental Model

If you want one summary sentence:

- `AzCore` and friends provide foundations.
- Gems package features.
- builders produce runtime assets.
- launchers boot applications.
- modules register functionality.
- the settings registry and related data wire startup together.

If any of those feel vague while reading the repo, jump back to the [main tutorial](./o3de-engine-study-tutorial.md) or the [staged labs](./staged-labs.md).
