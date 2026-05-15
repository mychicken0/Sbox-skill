# Coding Patterns

Use these patterns for any s&box game unless the local project already has a stronger convention.

## Architecture

- Prefer small `Component` classes with one responsibility.
- Use `GameObjectSystem<T>` for scene-wide services such as managers, registries, save/load hooks, cleanup, and spawn coordination.
- Use `GameResource` plus `[AssetType]` for designer-authored definitions: items, weapons, tools, shop entries, post-process presets, sounds, jobs, NPCs, terrain settings.
- Use prefabs for spawnable or reusable object graphs. Clone prefabs rather than reconstructing complex hierarchies in code.
- Keep runtime state on components; keep editable balance/configuration in `[Property]` fields or resources.

## Lifecycle

- Use `OnStart` for component initialization that depends on scene references.
- Use `OnUpdate` only for per-frame work that must run every frame; keep it cheap.
- Use `OnFixedUpdate` for physics-driven behavior.
- Use `OnDestroy` for cleanup, unregistering, and event detachment.
- For scene services, prefer explicit interfaces such as startup, save, physics, cleanup, or local project events when they exist.

## Editor-Friendly Data

- Add `[Property]` to references, tunables, and designer choices.
- Add `[Range]`, `[Group]`, `[Title]`, and asset types where they improve the editor workflow.
- Do not hardcode balance values if designers will tune them.
- Keep generated names predictable and useful in the hierarchy.

## Style

- Match the local folder layout and naming.
- Keep systems deterministic and easy to reason about.
- Prefer explicit validation and early returns.
- Use comments only for non-obvious intent or engine workarounds.
- Check DarkRP-style examples when available: small components, data resources, server validation, and practical UI that stays close to gameplay.
