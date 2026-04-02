# Staged Labs

These labs are designed to match the study order in the rest of this folder: reading first, optional setup later. The goal is to train your ability to trace systems through a large engine codebase before you try to modify or rebuild everything.

Companions:

- [Main tutorial](./o3de-engine-study-tutorial.md)
- [Repo map and reading order](./repo-map-and-reading-order.md)
- [MMORPG engine extraction](./mmorpg-engine-extraction.md)
- [90-day roadmap](./90-day-roadmap.md)

## Ground Rules

- Early labs require only reading and note-taking.
- Later labs can include optional build or tooling steps.
- If the O3DE Python environment is not bootstrapped yet, do not let that block the early labs.
- Prefer the root `README.md` for build steps when you are ready for them.
- If `scripts/o3de.bat` or `scripts/o3de.py` reports a missing venv, run `python\\get_python.bat` first or stay with the reading-only parts until later.

## Lab 1: Trace Engine Bootstrapping

Goal:

Understand how O3DE is assembled from the root and where the major product areas enter the build.

Read:

- `CMakeLists.txt`
- `engine.json`
- `Code/CMakeLists.txt`
- `Code/Framework/CMakeLists.txt`

Do:

1. Make a list of every top-level folder added by the root `CMakeLists.txt`.
2. Mark which ones are runtime-facing, tool-facing, data-facing, or extension-facing.
3. From `engine.json`, write down which Gems, templates, and built-in projects ship with the engine.
4. Sketch the relationship between `Code/Framework`, `Code/Editor`, `Code/Tools`, and `Gems`.

Deliverable:

Write a one-page map titled "How O3DE gets assembled."

What good looks like:

You can explain why O3DE is more than just `Code/Framework`, and you can name the files that define that shape.

## Lab 2: Trace A Core Abstraction Through AzCore

Goal:

Learn how to study a foundational engine abstraction through both source and tests.

Pick one:

- EBus
- entity/component lifecycle
- serialization/reflection

Read:

- `Code/Framework/AzCore/AzCore`
- `Code/Framework/AzCore/Tests/EBus.cpp`
- `Code/Framework/AzCore/Tests/Components.cpp`
- `Code/Framework/AzCore/Tests/EntityTests.cpp`
- `Code/Framework/AzCore/Tests/Serialization.cpp`

Do:

1. Identify the public-facing types or folders for your chosen abstraction.
2. Read the matching tests before going too deep into implementation.
3. Write down the abstraction's purpose in plain English.
4. Note one advantage and one cost of the design.

Deliverable:

A short note titled "What problem this AzCore abstraction solves."

What good looks like:

You can explain the abstraction to someone who has never seen O3DE, and you can point to both a source area and a test file that justify your explanation.

## Lab 3: Trace An Asset From Source To Runtime Product

Goal:

Understand how O3DE turns authored content into runtime-loadable data.

Suggested path:

- source asset family: `Gems/Terrain/Assets/Shaders/Terrain`
- builder side: `Gems/Atom/Asset/Shader`
- pipeline host: `Code/Tools/AssetProcessor`
- runtime-facing asset lookup: `Code/Tools/AssetProcessor/native/AssetManager`

Read:

- `Code/Tools/AssetProcessor/CMakeLists.txt`
- `Code/Tools/AssetProcessor/AssetBuilderSDK/AssetBuilderSDK/AssetBuilderBusses.h`
- `Code/Tools/AssetProcessor/native/AssetManager/AssetCatalog.h`
- `Gems/Atom/Asset/Shader/Code/Source/Editor/ShaderAssetBuilder.cpp`
- `Gems/Terrain/Assets/Shaders/Terrain/TerrainPBR_ForwardPass.shader`

Do:

1. Start with the source asset and describe what kind of runtime product it likely needs to become.
2. Read the builder contract in `AssetBuilderSDK`.
3. Read how the shader builder participates in that contract.
4. Read the asset management side and note how processed data becomes discoverable by runtime systems.

Deliverable:

A diagram showing `source asset -> builder -> product asset -> catalog -> runtime`.

What good looks like:

You no longer think of "loading an asset" as directly reading artist-authored source files.

Optional extension:

Compare the shader path with `Gems/Prefab/PrefabBuilder` and note where the pipeline pattern stays the same and where it changes.

## Lab 4: Trace A Render Path Through Atom

Goal:

Understand how O3DE layers rendering work from high-level feature request down toward backend abstractions.

Suggested path:

- high-level feature asset: `Gems/Terrain/Assets/Passes/TerrainParentPass.pass`
- shader asset family: `Gems/Terrain/Assets/Shaders/Terrain`
- engine-facing render layer: `Gems/Atom/RPI/Code/Source/RPI.Public`
- backend-facing render layer: `Gems/Atom/RHI/Code/Source/RHI`

Read:

- `Gems/Atom/gem.json`
- `Gems/Atom/RHI`
- `Gems/Atom/RPI`
- `Gems/Atom/Feature/Common`
- `Gems/Terrain/Assets/Passes/TerrainParentPass.pass`

Do:

1. Write down what seems to belong to RHI versus RPI.
2. Identify where pass and material concepts start to appear.
3. Identify where backend-specific implementations begin.
4. Note how Terrain uses the shared render stack instead of bypassing it.

Deliverable:

A layered diagram showing feature system, RPI, RHI, and backend.

What good looks like:

You can explain why a renderer usually needs more than a raw graphics API abstraction.

Optional extension:

Read one small test area under `Gems/Atom/RPI/Code/Tests/Pass` and note what kinds of behavior O3DE chooses to verify at that layer.

## Lab 5: Trace A Replicated Gameplay Component

Goal:

See how O3DE separates transport, serialization, and higher-level gameplay replication.

Suggested path:

- low-level transport/serialization: `Code/Framework/AzNetworking/AzNetworking`
- gameplay-facing replication: `Gems/Multiplayer/Code/Include/Multiplayer`
- tests: `Gems/Multiplayer/Code/Tests`

Read:

- `Code/Framework/AzNetworking/AzNetworking/Serialization/DeltaSerializer.h`
- `Code/Framework/AzNetworking/AzNetworking/TcpTransport/TcpNetworkInterface.h`
- `Gems/Multiplayer/Code/Include/Multiplayer/Components/NetworkTransformComponent.h`
- `Gems/Multiplayer/Code/Tests/NetworkTransformTests.cpp`
- `Templates/UnifiedMultiplayerGem/Template/README.md`

Do:

1. Describe what belongs to transport and what belongs to replicated gameplay state.
2. Trace `NetworkTransformComponent` from interface to test coverage.
3. Note where O3DE appears to assume authority, prediction, or hierarchy rules.
4. Note which parts would still be useful in a non-MMO multiplayer game and which parts point toward larger MMO concerns.

Deliverable:

A short note titled "What O3DE networking gives me, and what an MMO still needs beyond it."

What good looks like:

You can explain why an engine multiplayer layer is necessary but not sufficient for a full MMORPG stack.

## Lab 6: Write Your MMORPG Engine Cut List

Goal:

Turn study into decisions.

Use:

- [Main tutorial](./o3de-engine-study-tutorial.md)
- [MMORPG engine extraction](./mmorpg-engine-extraction.md)

Do:

Create four headings:

- keep
- simplify
- replace
- move outside the engine

Then fill each heading with at least five concrete items inspired by O3DE.

Prompts:

- Which O3DE ideas are clearly worth copying in principle?
- Which ideas are good but too large for a first engine?
- Which systems would you re-implement with a different shape?
- Which problems are not engine problems at all and belong in services or operations tooling?

Deliverable:

Your first architecture boundary document for your own engine.

What good looks like:

You leave the lab with a more realistic engine scope than the one you started with.

## Optional Later-Stage Hands-On Work

Once you are ready for setup and build work, use the root `README.md` as the baseline and then add these practical exercises:

- configure a build tree with CMake
- bootstrap O3DE Python if needed with `python\\get_python.bat`
- register the engine with `scripts\\o3de.bat register --this-engine`
- create a small test project or Gem from a template
- trace how a project-specific change flows through build, asset processing, and launcher startup

Do these only after the reading-based labs feel comfortable. The goal is to make setup deepen understanding, not replace it.
