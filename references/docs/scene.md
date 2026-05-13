 about

Scene

S&box uses a scene system, similar to Godot and Unity. Scenes are JSON files on disk that are fast to load

and switch between.

Everything in your game is built from Scenes, GameObjects, and Components working together.

Scenes

A Scene is your game world. Everything that renders and updates at one time should be in a scene. Scenes

can be saved to disk, loaded, and switched between at runtime.

GameObjects

A scene contains GameObjects — world objects with a position, rotation, and scale. They can be arranged

in a hierarchy so children move relative to their parents.

Components

GameObjects contain Components that provide modular functionality. A ModelRenderer renders a model,

a BoxCollider makes it solid. You create games by programming new Components.

GameObjectSystem

Systems that operate on GameObjects across an entire scene — useful for game managers and global

logic.

Pref abs

Reusable GameObject templates that can be instantiated at runtime or placed in scenes. Supports

instance overrides and nested prefabs.

Create d 14 Nov 2023

Updated 10 Apr 2026