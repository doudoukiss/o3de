# Repo Map And Reading Order

This document is the fast navigation companion for the O3DE study set. Use it when you want to know where a subsystem lives, what to read first, and what can safely wait until later.

Primary companions:

- [Main tutorial](./o3de-engine-study-tutorial.md)
- [Glossary and concepts](./glossary-and-concepts.md)
- [Staged labs](./staged-labs.md)
- [MMORPG engine extraction](./mmorpg-engine-extraction.md)
- [90-day roadmap](./90-day-roadmap.md)

## High-Level Map

| Area | Start Here | What You Learn |
| --- | --- | --- |
| Build and engine composition | `CMakeLists.txt`, `engine.json` | How the repo is assembled and what the engine ships with. |
| Core runtime | `Code/Framework` | Low-level engine foundations and shared runtime patterns. |
| Editor and tool bridge | `Code/Framework/AzToolsFramework`, `Code/Editor` | How authoring-time behavior is separated from runtime. |
| Asset pipeline | `Code/Tools/AssetProcessor`, `Code/Tools/SceneAPI` | How source assets become runtime products. |
| Rendering | `Gems/Atom`, especially `RHI` and `RPI` | How O3DE layers backend graphics and engine-facing rendering. |
| World systems | `Gems/Prefab`, `Gems/PhysX`, `Gems/Terrain`, `Gems/RecastNavigation`, `Gems/EMotionFX` | How authored worlds become simulated worlds. |
| Networking and multiplayer | `Code/Framework/AzNetworking`, `Gems/Multiplayer` | How transport and gameplay replication are separated. |
| Runtime entrypoints | `Code/LauncherUnified` | How projects boot as game, server, or unified launchers. |
| Templates | `Templates` | How O3DE expects projects and Gems to be extended. |
| Examples and tests | `AutomatedTesting`, `Tests` folders throughout the repo | Real usage and intent. |

## Recommended Reading Order

Follow this order for the first full pass through the codebase:

1. Read `CMakeLists.txt` and `engine.json`.
2. Read `Code/CMakeLists.txt` and `Code/Framework/CMakeLists.txt`.
3. Explore `Code/Framework/AzCore` and the tests in `Code/Framework/AzCore/Tests`.
4. Explore `Code/Framework/AzFramework` and `Code/Framework/AzGameFramework`.
5. Explore `Code/Framework/AzToolsFramework`, then `Code/Editor`, then `Code/Tools/ProjectManager`.
6. Read the structure of `Code/Tools/AssetProcessor` and `Code/Tools/SceneAPI`.
7. Move into `Gems/Atom`, starting with `RHI`, then `RPI`, then `Feature/Common`.
8. Study world-facing Gems: Prefab, PhysX, Terrain, RecastNavigation, EMotionFX.
9. Study `Code/Framework/AzNetworking`, then `Gems/Multiplayer`.
10. Read `Code/LauncherUnified` and then the relevant templates in `Templates`.

## Best First Files By Topic

### Build And Composition

- `CMakeLists.txt`
- `engine.json`
- `Code/CMakeLists.txt`
- `Code/Framework/CMakeLists.txt`

### Runtime Foundations

- `Code/Framework/AzCore/AzCore`
- `Code/Framework/AzCore/Tests/EBus.cpp`
- `Code/Framework/AzCore/Tests/Components.cpp`
- `Code/Framework/AzFramework/AzFramework`
- `Code/Framework/AzGameFramework/AzGameFramework`

### Editor And Tools

- `Code/Framework/AzToolsFramework/AzToolsFramework`
- `Code/Editor`
- `Code/Editor/Plugins`
- `Code/Tools/ProjectManager/CMakeLists.txt`
- `Code/Tools/SceneAPI`

### Asset Pipeline

- `Code/Tools/AssetProcessor/CMakeLists.txt`
- `Code/Tools/AssetProcessor/AssetBuilderSDK/AssetBuilderSDK/AssetBuilderBusses.h`
- `Code/Tools/AssetProcessor/native/AssetManager`
- `Code/Tools/SceneAPI`
- `Gems/Atom/Asset/Shader/Code/Source/Editor/ShaderAssetBuilder.cpp`
- `Gems/Prefab/PrefabBuilder/PrefabBuilderComponent.cpp`

### Rendering

- `Gems/Atom/gem.json`
- `Gems/Atom/RHI/Code/Source/RHI`
- `Gems/Atom/RPI/Code/Source/RPI.Public`
- `Gems/Atom/Feature/Common`
- `Gems/Terrain/Assets/Passes/TerrainParentPass.pass`

### Networking And Multiplayer

- `Code/Framework/AzNetworking/AzNetworking/Framework`
- `Code/Framework/AzNetworking/AzNetworking/Serialization/DeltaSerializer.h`
- `Code/Framework/AzNetworking/AzNetworking/TcpTransport/TcpNetworkInterface.h`
- `Gems/Multiplayer/Code/Include/Multiplayer`
- `Gems/Multiplayer/Code/Tests`
- `Templates/UnifiedMultiplayerGem/Template/README.md`

### World Simulation

- `Code/Framework/AzFramework/AzFramework/Spawnable`
- `Gems/Prefab/PrefabBuilder`
- `Gems/PhysX/Common`
- `Gems/PhysX/Core`
- `Gems/Terrain`
- `Gems/RecastNavigation/Code/Include/RecastNavigation`
- `Gems/EMotionFX/Code`

## How To Read Each Subsystem

When you open a new subsystem, use the same reading pattern:

1. Start with `CMakeLists.txt` and any `gem.json`.
2. Identify public include folders and test folders.
3. Find the runtime-facing entrypoints first.
4. Only then descend into implementation details.
5. End by reading tests and writing down the subsystem's responsibilities.

This helps prevent the classic engine-study trap where you read implementation before you know the boundary.

## Lower-Priority Areas On The First Pass

These are worth studying later, but they should not block your first understanding of the engine:

- `Code/Legacy`
- Platform-specific subfolders under `Platform/*`
- DCC scripting and external content creation integrations under `Gems/AtomLyIntegration`
- UI and platform service Gems that are not central to your own engine goals
- Marketplace-style or service Gems unrelated to runtime architecture

None of these are unimportant. They are just lower leverage for a first pass aimed at engine architecture.

## A Good First-Pass Goal

After the first pass, you should be able to answer:

- How does O3DE boot?
- What are the framework layers?
- How do tools differ from runtime?
- How do assets become runtime data?
- How is rendering layered?
- How are networking and replication split?
- Which systems would matter most to an MMORPG engine?

If you can answer those clearly, you are ready for the [staged labs](./staged-labs.md) and the [MMORPG extraction guide](./mmorpg-engine-extraction.md).
