---
name: sbox-skill
description: General s&box game development skill for C#, Scene System GameObject/Component architecture, GameObjectSystem services, networking, RPC, Sync, GameResource data assets, prefabs, Razor UI, SCSS, materials, shaders, .shdrgrph Shader Graph assets, post-processing, and editor tooling. Use when Codex builds, fixes, reviews, or explains any s&box game code or asset workflow.
---

# s&box Agent Guide

Build for modern s&box. Start from the project in front of you, prefer editor-friendly systems, and keep multiplayer authority secure.

## First Moves

1. Read local rules first: `AGENTS.md`, `PRODUCT.md`, `.sbproj`, and nearby feature files.
2. Search for similar systems before inventing patterns. Use `rg` in the project's `Code/`, `Assets/`, and `Libraries/` folders for examples of player spawning, UI state, inventory, weapons, resources, shaders, post-processing, save/load, and networking.
3. Inspect prefabs, resources, materials, shaders, Razor panels, and existing folder naming when relevant.
4. Reuse local managers, helpers, extension methods, resource types, and naming conventions instead of creating parallel systems.
5. Keep changes scoped to the requested feature; do not refactor unrelated systems.

## Core Rules

- Use Scene System only: `GameObject`, `Component`, `GameObjectSystem<T>`, prefabs, and scene events.
- Expose tunable data with `[Property]`, `GameResource`, editor ranges, groups, and clear asset names.
- Never trust clients. Host/server validates client requests and owns meaningful state changes.
- Use `[Sync]` for replicated state, `[Rpc.Host]` for client-to-host requests, and `[Rpc.Broadcast]` for host-approved fanout.
- Guard authority with `Networking.IsHost`, `!IsProxy`, `GameObject.IsProxy`, owner checks, or `Rpc.Caller` validation as appropriate.
- Avoid fragile engine hacks: no private reflection, no internal method invocation, no generated binary hand-edits.
- Prefer readable, explicit components over clever abstractions.

## Load References As Needed

- General C#/architecture: `references/coding-patterns.md`
- Common API snippets: `references/api-cheatsheet.md`
- Core class reference: `references/core-api.md`
- Multiplayer/security: `references/networking-security.md`
- Data assets/prefabs: `references/resources-and-prefabs.md`
- Razor UI/SCSS: `references/ui-razor.md`
- Physics/traces/collisions: `references/physics-and-traces.md`
- Materials, shaders, Shader Graph, post-processing: `references/shaders-and-postprocess.md`
- Shader Graph JSON/node snippets: `references/shadergraph-snippets.md`

## Validation Habit

- Build or run targeted tests when available.
- For asset JSON such as `.shdrgrph`, validate JSON and references after editing.
- If s&box editor generation is required, say so clearly instead of pretending a CLI compile verified it.
- If a needed API is missing from these snippets and local code does not answer it, use official docs/search at `https://wiki.facepunch.com/sbox/` before guessing.
