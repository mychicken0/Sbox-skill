# sbox-skill

A lean CLI/Agent skill for building modern **s&box** games

This skill helps agents work with:

- C# `GameObject` / `Component` architecture
- `GameObjectSystem<T>` services
- `[Property]` editor configuration
- `GameResource` data assets
- prefabs and scene workflows
- server-authoritative networking with `[Sync]`, `[Rpc.Host]`, and `[Rpc.Broadcast]`
- Razor UI and SCSS
- materials, post-processing, shaders, and `.shdrgrph` Shader Graph files

The goal is practical agent behavior, not a huge documentation archive. The bundled references are curated snippets and patterns that help Codex write correct code faster.

## Install Into One s&box Project

Use this when you want the skill to apply to a specific game or gamemode repository.

```powershell
git clone https://github.com/mychicken0/Sbox-skill.git .agents\skills\sbox-skill
```

Restart CLI/Agent or open a new CLI/Agent thread in that project. The skill should appear as `sbox-skill`.

## Update

Project-local install:

```powershell
git -C C:\path\to\your\sbox_project\.agents\skills\sbox-skill pull
```

## Recommended Project Setup

For best results, keep project guidance in your game repository too:

- `AGENTS.md` for repo-specific agent rules
- `PRODUCT.md` for game direction, tone, and design goals
- a clear `.sbproj` at the project root
- consistent folders for `Code/`, `Assets/`, resources, prefabs, UI, shaders, and materials

The skill tells Codex to inspect those files first, then search local code before inventing new patterns.

## Notes For Shader Work

When asking Codex for shader or post-process work, it can often edit or provide `.shdrgrph` Shader Graph JSON instead of hand-writing shader code. This is usually less error-prone because the s&box Editor can save and generate the compiled outputs.

Keep C# attribute names stable when editing shader graphs, for example `DirtStrength`, `TintColor`, `RimThickness`, or any names your components already send through `RenderAttributes`.

## What Is Included

- `SKILL.md` - the main agent instructions
- `references/` - small curated snippets for coding patterns, networking, UI, resources, physics, shaders, and core API reminders

Large dumped docs are intentionally not included. If the snippets are not enough, the skill instructs agents to inspect local project code first, then use the official s&box docs at `https://wiki.facepunch.com/sbox/`.
