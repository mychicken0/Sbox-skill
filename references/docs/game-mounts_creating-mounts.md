 about

Creating Mounts

The mount system is extensible - anyone can write a mount to add support for a new game or engine and

contribute it to s&box via pull request. A mount detects a game's install directory via Steam, scans its files,

and converts assets into s&box compatible assets, all at runtime.

Overview

The mounting system is built on two key classes:

BaseGameMount — detects the game and registers assets during mount

ResourceLoader — loads and converts individual assets on demand

Mounts live in the s&box engine under the engine/Mounting/ folder. To add support for a new game or

engine, create a new mount project, code it and submit a pull request.

Creating a Game Mount

Extend BaseGameMount and implement the required properties and methods:

public class MyGameMount : BaseGameMount
 public override string Ident => "rust";
 public override string Title => "Rust";

 private string GameDir;

 protected override void Initialize( InitializeContext context )
 // Check if the game is installed via Steam
 if ( !context.IsAppInstalled( 252490 ) )
 return;

 GameDir = context.GetAppDirectory( 252490 );
 IsInstalled = true;

 protected override Task Mount( MountContext context )
 // Scan game files and register each resource
 foreach ( var file in Directory.GetFiles( GameDir, "*.mymodel", SearchOption.A
 var relative = Path.GetRelativePath( GameDir, file );
 context.Add( ResourceType.Model, relative, new MyModelLoader( this, file )

 IsMounted = true;
 return Task.CompletedTask;

Ident and Tit le

Ident is a unique lowercase identifier for your mount (e.g. "quake" , "hl1" ). It's used in mount:// paths

and project config. Title is the display name shown in the editor.

Init ialize

Called at startup to detect whether the game is installed. Use context.IsAppInstalled(appId) to check

Steam, and context.GetAppDirectory(appId) to get the install path. Set IsInstalled = true if the game

is found.

Mount

Called when the user enables the mount. Scan the game's files and register each resource with

context.Add() . Set IsMounted = true when done.

Creating Resource Loaders

Each resource type needs a ResourceLoader that converts the game's native format into something

s&box understands. Resources are loaded lazily - Load() is only called when the asset is actually used.

public class MyModelLoader : ResourceLoader<MyGameMount>
 private string FilePath;

 public MyModelLoader( MyGameMount host, string path )
 FilePath = path;

 protected override object Load()
 // Read the file and convert it to an S&box model
 var data = File.ReadAllBytes( FilePath );
 return ConvertToModel( data );

Use the generic ResourceLoader<T> to get typed access to your mount instance via the Host property.

Async Loading

For resources that take time to load, override LoadAsync instead:

protected override async Task<object> LoadAsync()

 return ConvertToModel( data );

Resource T ypes

Register resources using the ResourceType enum:

T yp e

S & b o x Ex t e ns io n

D e s c r ip t io n

Model

Texture

Material

Sound

Scene

.vmdl

.vtex

.vmat

.vsnd

.scene

PrefabFile

.prefab

Resource Flags

3D models with meshes, skeletons, animations

Textures and images

Materials referencing textures

Audio files

Scene files

Prefab files

You can set flags on resources to control their behavior:

var loader = new MyModelLoader( this, file );
loader.Flags = ResourceFlags.DeveloperOnly; // Only visible in asset browser, not in-g

F la g

D e s c r ip t io n

DeveloperOnly

Hidden from game, only visible in the asset browser

NeverRagdoll

Don't treat this model as ragdollable

Effect

Non-solid, no physics

Create d 19 Apr 2026

Updated 19 Apr 2026