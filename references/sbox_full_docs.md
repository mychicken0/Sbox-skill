 about

FAQ

How do I get it?

We'll be releasing s&box on Steam on the 28th April for $20.

Access to the developer preview is now closed — you may or may not get to keep it post release

depending on play time, development or skins purchased.

Are you using workshop?

No. We've made a system where you don't have to install addons. This is what sbox.game is. In the same

way, you don't have to install videos from YouT ube; you just download what you need.

Why not Unity? Why not UE?

We're sentimental about the Source engine. Source 2 has a beautiful renderer and brings the engine up to

date with tools like ModelDoc and Animgraph.

It would have been cheaper and easier to do thisall on Unity or UE, but we would have loved it less.

Will creators beable to monetize?

Yes. It's integral. We owe our entire business to the fact that Valve let us monetize.

Right now there are two ways for our creators to make money. You can make a cosmetic item, which then

goes for sale in game and you get a cut of it via Steam Workshop. Or you can make a game and get a cut

of the playfund.

We want to be careful about pushing further. We want you to beable to charge for whatever you want,

but we also don't want everything to become pay-to-win like on other platforms.

So is it an engine, or a platf orm?

It's everything. An explanation was posted on this blog here.

Create d 13 Fe b 2024

Updated 5 Se p 2025 about

Component Actions

The easiest way to add an ActionGraph to your scene is through the Actions Invoker component. Just click

Add Component on an object, then you can find it under Actions.

You can also find action properties in a few other built-in components, like Colliders when Is Trigger is

checked.

Each of these start out with an "Empty Action". Simply click on any of those to create a new ActionGraph

and start editing it!

T ake a look at the Intro to ActionGraphs guide to learn how to edit your new graph.

Create d 8 Jan 2024

Updated 9 O ct 2024 about

Custom Nodes

T here are two ways to create your own node types:

Action Resources

C# Method Nodes

Create d 9 Jan 2024

Updated 23 Jan 2024 about

Examples

Here's how to do some common things. Each has a code you can copy to your clipboard, then Ctrl+V to

paste in the ActionGraph editor.

Loop T hrough Child Objects

Clipboard Code

actiongraph:H4sIAAAAAAAACp1UW0+DMBR+X7L/0OArQ5huGb4ZTcyi0SVeXoxZCpyxKrSkLWbLwn+3pbjVMc

Move With Velocity

Clipboard Code

actiongraph:H4sIAAAAAAAACr1U30+DMBB+X7L/gfDMENjGmG8mJsZodIlzL8YsBaqpQkvabnFZ9r/b0g2qDA

Updated 9 Jan 2024 about

Getting Started

ActionGraph is a visual scripting language. Each node describes an action or expression, and links between

nodes carry values or signals.

Creating a new ActionGraph

To start using ActionGraph in your project, you can either:

Use the built-in Component actions

Use the Component Editor to create methods in a custom component

Add a Delegate-type property to a custom component in C#

Following either guide above will get you into the ActionGraph editor.

Nodes

Nodes appear as rectangles in the ActionGraph editor with a name (or symbol), and input or output

sockets. You create a node by right-clicking in any empty space, or dragging a link from an output to get a

list of possible nodes that are specific to the link value type.

The root node is the entry point of your graph. It'll be the only node in a new graph, and can't be deleted. It

has only output sockets: one signal socket at the top, and optionally some value sockets if your graph

accepts parameters.

When the graph runs, a signal is fired from the output signal socket of your root node. This will follow any

links to other action nodes, causing them to run too.

Expression Nodes

Expression nodes (green) perform a calculation based on their inputs, without changing any state

elsewhere. They don't have any input or output signal sockets, and will evaluate when any of their output

values are used by another node.

Action nodes (blue) are any nodes with the white, arrow-shaped signal sockets. These nodes trigger things

to happen when receiving a signal.

Most action nodes will have one input and one output signal socket in their title bar. The input will trigger

the node to run, and the output will fire when the node has finished performing its action.

Some control flow nodes like If, While, For Each, or For Range, will have extra output signal sockets that will

fire if certain conditions are met. This allows you to do loops, or branch based on some condition.

Links

Links connect an output of one node to an input of another. A link between signal sockets (white, arrow-

shaped) will carry a signal, and any other link will carry a value. Links are created by dragging from a node's

output.

If your graph is becoming messy because of links travelling a long distance, you can use variables to help

clean things up. You can also use reroute nodes (shift-click on an existing link) to help organize your links.

Your graph can't be linked in a way that leads to a cycle: it shouldn't be possible to follow links from outputs

to inputs and arrive back at the same node. You can use special action nodes in the Control Flow category

to perform loops, rather than trying to connect your nodes in a cycle with links.

Constants

If you want to use a hard-coded value in an input, you can directly set it in the Properties panel when the

node is selected.

Now you know the basics, the next things to learn are:

How to use variables

Creating your own custom nodes

Create d 8 Jan 2024

Updated 19 Apr 2026 about

ActionGraph

ActionGraph is a visual scripting system that lets you create game logic using nodes instead of code.

Connect nodes together to build behaviors, respond to events, and control your scene — all from a

graphical editor.

What Can You Do?

Script without code — build gameplay logic, UI interactions, and event handling visually

React to events — trigger graphs from collisions, input, timers, or custom C# delegates

Control f low — use loops, branches, and delays to create complex behaviors

Mix with C# — call ActionGraphs from code or expose C# methods as custom nodes

Reuse logic — save graphs as action resources and share them across your project

How It Works

Every ActionGraph starts with a root node that fires a signal when the graph runs. You connect action

nodes (blue) to perform operations in sequence, and expression nodes (green) to compute values.

Links between nodes carry signals or data.

like trigger collisions, or invoked directly from C# using delegate properties.

Pages

🌱 Getting Started — learn the basics of nodes, links, and graph editing
🧩 Component Actions — add ActionGraphs to your scene with built-in components
💾 Variables — store and reuse values in your graphs
🛠 Using With C# — invoke graphs from code and pass parameters
📖 Examples — copy-paste examples for common patterns
🆕 Custom Nodes — create your own node types

Create d 8 Jan 2024

Updated 19 Apr 2026 about

Using With C#

Here's how you can use ActionGraph with your game code written in C#.

public class ExampleComponent : Component

[Property]
public Action ExampleAction { get; set; }

protected override void OnUpdate()

if ( Input.Down( "attack1" ) )

ExampleAction?.Invoke();

Declaring the Property

[Property]
public Action ExampleAction { get; set; }

This will add a property that we can see in the inspector. For a property to be usable as an ActionGraph it

must have a Delegate type. We're using the type Action here, which takes in no parameters and returns

nothing. Once we do this we can press the "+" to add as many callbacks to the Action as we want.

will show only the one action in-line without having the option to add/remove others.

Clicking on the Example Action or Empty Action will open the ActionGraph editor and start editing it.

Adding Paramet ers

If you want to beable to pass in some parameters, you can use a different delegate type:

[Property]
public Action<int, string, GameObject> ExampleAction { get; set; }

declared them.

Renaming Paramet ers

T here's a couple of ways to rename the parameters, since "Arg 1", "Arg 2" isn't very helpful. First, you can

click on the root node in the editor, and change the socket names and descriptions in the Properties panel.

The other way is to use a custom delegate type:

public delegate void ExampleDelegate( int someNumber, string someText, GameObject some

[Property]
public ExampleDelegate ExampleAction { get; set; }

This will automatically fill in the names of each parameter like above, and you can re-use the same

delegate type for any property that would take in the same set of parameters.

Running an ActionGraph

You can call the property like any other method directly:

ExampleAction();

However, if the action hasn't been created in the editor yet, this will throw a NullReferenceException . A

safer way to run it is to check for null like this:

This is shorthand for:

if ( ExampleAction is not null ) ExampleAction();

Passing in Argument s

If you've declared some parameters, you can pass in values when running the graph like this:

ExampleAction( 123, "Hello, World!", GameObject.Parent );

Or if you're checking for null:

ExampleAction?.Invoke( 123, "Hello, World!", GameObject.Parent );

Ret urning Values

Delegates with return types are supported too.

[Property]
public Func<int> TestExpression { get; set; }

Graphs implementing delegates like this will have an Output node, which you'll need to connect to the

input without going through any async nodes (like delays).

Async Graphs

If you want to wait for a graph with delays to finish running, it needs to be declared with a delegate type

that returns a T ask.

[Property]
public Func<Task> ExampleAction { get; set; }

With parameters:

[Property]
public Func<int, string, GameObject, Task> ExampleAction { get; set; }

public delegate Task ExampleDelegate( int someNumber, string someText, GameObject some

[Property]
public ExampleDelegate ExampleAction { get; set; }

When you call it you can either await the returned task, or use ContinueWith outside of async code.

await ExampleAction( 123, "Hello, World!", GameObject.Parent );

ExampleAction?.Invoke( 123, "Hello, World!", GameObject.Parent )
 .ContinueWith( task => { } );

Next Steps

T ake a look at the Intro to ActionGraphs guide to learn how to edit your new graph.

Create d 8 Jan 2024

Updated 2 Jun 2025 about

Variables

Variables are useful for making your graph easier to understand, cleaning up link spaghetti, and when

performing calculations in loops.

You can create a new variable by dragging a link from an output with the value type you want the variable

to hold, selecting "Add Variable", then giving it a name.

create more nodes to get or set the value of the variable by righ-clicking, then looking under Variables.

You can also directly use a variable in an input socket by right-clicking on it, then selecting the variable

from the context menu.

Create d 9 Jan 2024

Updated 29 Apr 2024 about

Animation

S&box uses Valve's Animgraph system for character animation, providing a powerful node-based

animation state machine. The system supports skeletal animation, IK, animated ragdolls, morph targets,

and animation events.

Key features:

Animgraph — node-based animation state machines

Skeletal animation and blending

Inverse Kinematics (IK)

Animated ragdolls

Morph targets

Animation events

Movie Maker

Movie Maker is a timeline-based editor for animating properties in a scene. It's ideal for in-game

cutscenes, editing trailers, coordinating timed events, and creating skeletal animations — all without

leaving the editor.

Create d 10 Apr 2026

Updated 11 Apr 2026 about

Assets

Assets are the building blocks of your game — models, materials, sounds, textures, and custom resources.

S&box provides tools for creating, importing, managing, and distributing assets.

Clothing

Create and publish cosmetic clothing items for the Citizen character model.

Ready-to-use Assets

Built-in assets provided by s&box, including Citizen characters and first-person weapon models.

Resources

Custom asset types, cloud assets, binary serialization, and GameResource extensions.

File System

Reading and writing files for user data and game saves.

Storage (UGC)

User-generated content storage and distribution.

Create d 15 Jun 2025

Updated 10 Apr 2026 about

Code

S&box games are written in C#. The engine features a hotload system that compiles and applies your

code changes within milliseconds, so you can iterate without restarting.

Code Basics

Cheat sheets, math types, console variables, and API whitelist information to get you productive quickly.

Advanced T opics

Code generation, hotloading internals, and unit testing.

Libraries

How to use and create reusable code libraries for your projects.

Create d 15 Jun 2025

Updated 10 Apr 2026 about

Editor

The s&box editor is your workspace for building games — scene editing, asset management, visual

scripting, and more.

ActionGraph

Visual scripting system for creating logic without writing code.

Editor T ools

Custom tools you can build to extend the editor for your game's needs.

Mapping

Hammer-based map creation with brushwork, props, lights, and GameObjects.

Model Editor

ModelDoc-based model editing and configuration.

More

Editor Shortcuts — Keyboard shortcuts

Editor Apps — Custom editor applications

Editor Widgets — Widget-based editor UI

Custom Editors — Custom inspector editors

Property Attributes — Inspector customization

Asset Previews — Custom asset preview rendering

T exture Generators — Procedural textures

Undo System — Undo/redo for editor operations

Editor Events — Editor lifecycle hooks

Editor Project — Editor project structure

Create d 29 De c 2023

Updated 10 Apr 2026 about

Exporting Standalone

Exporting standalone games is currently in preview. Distribution requires approval from Valve -

we're working with them to open this up to everyone. In the meantime, please don't distribute

exported builds without a license from us (contact garry@facepunch.com).

Export your game as a standalone executable and distribute it outside of the s&box platform.

Steam and beyond - publish to any storefront, as long as it's also on Steam

No engine royalties - the engine is completely royalty-free, no revenue share

Open source engine - full access to the engine source code

PC Only - we don't have any console or mobile exports right now, this could always change in the

future

Full .NET access - no code whitelist, use any .NET API

Standalone games have no code whitelist restrictions and some additional APIs. See Standalone Code for

details.

Export Wizard

2. Click Export…

3. Set your icon, splash screen, and Steam App ID

4. Click Next and wait for the export to complete

5. Your executable will be in the output folder — click Open Folder to find it

Create d 10 O ct 2025

Updated 26 Apr 2026 about

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

Updated 19 Apr 2026 about

Game Mounts

Game Mounts let users play with assets from other games they have installed inside s&box. Models,

textures, materials, and sounds are converted on-the-fly - no manual importing or file conversion required.

Mounted assets are runtime only, it's not possible to publish or ship them with games. Players need to own

and install the original games on Steam to play with the assets.

How It Works

Each mount is a plugin that knows how to find and convert assets from a specific game. When you enable

a mount, it detects the game's install directory via Steam, scans for assets, and converts them into s&box

compatible assetsall at runtime. Mounted assets are accessed via mount:// paths and lazy-loaded on

demand.

Mounts are toggled in the Asset Browser or used in the Sandbox Spawn Menu. The system is extensible

- anyone can write a new mount and contribute it to s&box via pull request.

Create d 19 Apr 2026

Updated 19 Apr 2026 about

Clutter

The Clutter System lets you quickly scatter large amounts of small objects like grass, rocks, and debris

across your scene. It handles placement, streaming, and GPU-instanced rendering for models

automatically.

Clutter Resource

A Clutter Definition is an asset that describes what to scatter and how. Create one from the Asset Browser

via Create > Clutter Def inition.

Ent ries

A list of models or prefabs to scatter. Each entry has a Weight value that controls how likely it is to be

picked relative to other entries. Use models for simple static props like grass or rocks, and prefabs when you

need components or behaviors.

Scat t erer

Controls how entries are distributed across the surface.

D e s c r ipt io n

Simple

Slope

T errain

Mat erial

Random placement with configurable density, scale range, ground alignment, and height

offset. Good for most use cases.

Filters entries by surface angle. Map different entries to different slope ranges e.g. grass on

flat ground, rocks on steep slopes.

Places entries based on the terrain material at each point. Map specific entries to specific

terrain layers. e.g. flowers on dirt, moss on rock.

It is possible to extend and implement your own scatterer in case you need more scattering

rules. e.g. using splines, volumes, or textures to drive the scattering

St reaming

Controls the tile grid used for generation and streaming:

T ile Size: Size of each generation tile (256–4096 units). Larger tiles mean fewer generation jobs but

coarser streaming granularity.

T ile Radius: How many tiles around the camera to keep populated (1–10). Controls the visible range

of clutter.

Clut t er Component

Add a ClutterComponent to a GameObject in your scene and assign a Clutter Definition. It has two

modes:

M o d e

Inf init e

Volume

D e s c r ipt io n

Streams tiles around the camera automatically. Tiles are created and destroyed as the camera

moves. Use this for open-world ground cover.

Generates clutter within a fixed bounding box. Click Generat e to populate. Instances are saved

with the scene.

In Inf inite mode, the system automatically regenerates tiles when the terrain is modified underneath

them.

Clut t er T ool

The Clutter T ool in the editor toolbar lets you paint and erase clutter instances by hand.

Paint: Left-click to scatter instances at the brush location using the assigned scatterer.

Erase: Ctrl+click to remove instances within the brush radius.

The brush has Size and Opacity settings. Opacity controls how many of the generated candidates are

actually placed, letting you thin out placement for a more natural look.

Painted instances are stored separately from generated ones and persist with the scene.

Updated 3 Apr 2026newspaper about games games business_center workshop

Controller Input

Some Input methods are specific to Controllers/Gamepads, and are useful to know for making sure your

player experience caters to those who don't play on a Keyboard + Mouse.

To see if the player is using a Controller, you can check Input.UsingController

Analog Inputs

You can get direct analog inputs from the Left Stick, Right Stick, Left T rigger or Right T rigger. Keep in mind

that notall Controllers have analog triggers.

float moveX = Input.GetAnalog( InputAnalog.LeftStickX );
float aimAmount = Input.GetAnalog( InputAnalog.LeftTrigger );

T here is also Input.AnalogMove and Input.AnalogLook which are Vector3 and Angles respectively that

automatically map to both the Keyboard + Mouse and the Left and Right Stick.

Haptics/Rumble

You can directly set the vibration intensity of each motor (and how long the vibration should last)

float leftMotor = 0.5f; // 50% intensity
float rightMotor = 0.7f; // 70% intensity
float leftTrigger = 0.2f; // 20% intensity
float rightTrigger = 0f; // No vibration
int duration = 1000; // 1000 milliseconds == 1 second

Input.TriggerHaptics( leftMotor, rightMotor, leftTrigger, rightTrigger, duration );

Or you can use one of a few presets, specifying the length, frequency and intensity

// These are optional inputs
float lengthScale = 1.2f; // 1.2x longer vibration time
float frequencyScale = 2f; // 2x vibration frequency
float amplitudeScale = 0.5f; // 0.5x as intense of a rumble

Input.TriggerHaptics( HapticEffect.HardImpact, lengthScale, frequencyScale, amplitudeS
menu

Motion Controls

If the Controller has a gyroscope or an accelerometer, then you can get motion data, otherwise it will be

null.

InputMotionData motionData = Input.MotionData;
if(motionData is not null)
 Vector3 acceleration = motionData.Acceleration; // Accelerometer
 Vector3 angularVelocity = motionData.AngularVelocity; // Gyroscope
 // Process the data as needed...

Local Multiplayer

You can see how many Controllers are currently connected using Input.ControllerCount

With that count you could create a Player GameObject for each index, and then query their Inputs as

normal

int playerIndex = 0; // The index of the controller this player is using

using( Input.PlayerScope( playerIndex ) )
 // Any input handling within this code block will only query Controller index 0
 if( Input.Pressed( "Jump" ) )
 // Make Player 1 jump (or whichever index)

Create d 25 Fe b 2025

Updated 25 Fe b 2025

menu

menu about

Glyphs

Input glyphs are an easy way to show users which buttons to press for actions, they automatically adjust

for whatever device you're using and return appropriate textures.

Texture JumpButton = Input.GetGlyph( "jump" );

Glyphs can change from users rebinding keys, or switching input devices - so it's worth it just

grabbing them every frame.

You can also choose between the default and outlined versions of glyphs, like so:

Texture JumpButton = Input.GetGlyph( "jump", true );

To use these quickly and easily in razor, you can use the resulting texture directly in an <Image> panel:

<Image Texture="@Input.GetGlyph( "jump", InputGlyphSize.Medium, true )" />

Examples

Updated 10 Jul 2025 about

Input

Input is accessed using the… Input class!

public sealed class MyPlayerComponent : Component

protected override void OnUpdate()

if ( Input.Down( "jump" ) )

WorldPosition += Vector3.Forward * Time.Delta;

Here you can see that when jump is pressed down, the GameObject will move forward. We multiply forward

by the time delta to make it frame rate independent.

T here are a few different ways to query buttons..

Input.Down( "jump" ) // key is held down (button name is case insensitive)
Input.Pressed( "jump" ) // key was just pressed this frame
Input.Released( "jump" ) // key was just released this frame

Input.AnalogMove // joystick "move" input Vector3 (or wsad)
Input.AnalogLook // Joystick "look" input Vector3 (mouse look)

Custom Keys

You can customize the keys for your game in the Project Settings.

By default, s&box will show the pause menu when a player presses the ESC key in-game.

You can override this functionality:

// In Update() on one of your components
if ( Input.EscapePressed )

Input.EscapePressed = false;
// handle escape pressed in your game

If you override the escape button it'll be up to you to let the user access settings etc in your own menu

system.

Create d 28 De c 2023

Updated 15 Jun 2025 about

Raw Input

We very much recommend that you only use this if you can't use input actions for whatever

reason. You can't rebind these atall.

We have the ability to access keyboard inputs directly, bypassing input actions.

// Is the W key down this frame?
if ( Input.Keyboard.Down( "W" ) )
 Log.Info( "W is down!" );

// Was the W key pressed this frame?
if ( Input.Keyboard.Pressed( "W" ) )
 Log.Info( "W was pressed!" );

// Was the W key released this frame?
if ( Input.Keyboard.Released( "W" ) )
 Log.Info( "W was released!" );

Most of the keys on the keyboard should work, here's an exhaustive list of them.

Ke y

Na me

"0" - "9"

"a" - "z"

"KP_0" - "KP_9"

"KP_DIVIDE"

0 - 9

A - Z

Numpad 0 - Numpad 9

Numpad /

Na me

"KP_MULTIPLY"

"KP_MINUS"

"KP_PLUS"

"KP_ENTER"

"KP_DEL"

"SEMICOLON"

"ENTER"

"SPACE"

"BACKSPACE"

"TAB"

"CAPSLOCK"

"NUMLOCK"

"ESCAPE"

"SCROLLLOCK"

"INS"

"DEL"

"HOME"

"END"

Numpad *

Numpad -

Numpad +

Numpad Enter

Numpad Delete

Less Than

More Than

Left Bracket

Right Bracket

Semicolon

Apostrophe

Backtick / Console Key

Comma

Period

Slash

Backslash

Hyphen / Minus

Equals

Enter

Space

Backspace

Tab

Caps Lock

Num Lock

Escape

Scroll Lock

Insert

Delete

Home

End

Na me

Page Up

Page Down

Pause

Left Shift

Right Shift

Left Alt

Right Alt

Up Arrow

Left Arrow

Right Arrow

Down Arrow

"PGUP"

"PGDN"

"PAUSE"

"SHIFT"

"RSHIFT"

"ALT"

"RALT"

"UPARROW"

"LEFTARROW"

"RIGHTARROW"

"DOWNARROW"

Create d 7 Apr 2025

Updated 15 May 2025 about

Gameplay

Core gameplay systems — input, navigation, terrain, and more.

Input

Keyboard, mouse, and controller input handling.

Navigation

NavMesh generation, pathfinding agents, areas, and links.

T errain

T errain creation, editing, and materials.

Clutter

Procedural detail placement on terrain.

VR

Virtual reality setup and components.

Create d 10 Apr 2026

Updated 10 Apr 2026 about

Navigation

We implement Recast Navigation in s&box, the industry standard for navmesh generation and navigation

agents. It's used in Unreal, Unity and Godot. So if it seems familiar, that's why.

What is a NavMesh?

A NavMesh is a simplified map of traversable areas in a game world, designed to help AI with pathfinding

and movement. NavMeshes are created from the game's PhysicsWorld, which defines where AI

characters are allowed to move.

Understanding NavMesh Limitations

A NavMesh is not a detailed or precise representation of the game world; rather, it is a simplified

abstraction focused solely on navigable areas. It lacks exact height information or precise ground

geometry. Use the PhysiscsWorld alongside the NavMesh, for interactions that require specific physical

details, such as placing the game object on the ground.

Creating a NavMesh

To create a NavMesh in your scene, just click the Enable NavMesh button in the header.

The NavMeshis split up into multiple smaller tiles. The ==yellow== lines represent regular polygon

boundaries, while the ==blue== lines represent polygon borders that are also tile boundaries.

NavMesh Settings

You can edit further NavMesh settings by clicking the pencil and paper icon in the NavMesh group in the

header.

physics objects are used when generating the mesh.

Code

The navmesh is accessible at Scene.NavMesh .

// Get a random position anywhere the navmesh
var pos = Scene.NavMesh.GetRandomPoint();

// Get a random position within radius of testposition
var pos = Scene.NavMesh.GetRandomPoint( testposition, radius );

// Get the closest point on the navmesh from another position
var pos = Scene.NavMesh.GetClosestPoint( testposition );

// Get the closest edge of the navmesg from this position
var pos = Scene.NavMesh.GetClosestEdge( testposition );

// Get a path from one position to another
var path = Scene.NavMesh.CalculatePath( new CalculatePathRequest()

Agent = Agent, // Optional agent to use for parameters

 Start = WorldPosition,
 Target = TargetWorldPosition

// Path.Status is either Complete or Partial
if ( path.IsValid() ) // ...

// Mark the navmesh dirty, so it will be rebuilt in the background
Scene.NavMesh.SetDirty();

Create d 2 Fe b 2024

Updated 3 Nov 2025 about

NavMesh Agent

A NavMesh Agent will move from position to position on the NavMesh, automatically. It features crowd

control features, so they will try to avoid bumping into each other if possible.

Component

over control of the position and rotation.

You would usually create another component, for your main AI logic, which will set positions and animate a

model based on its velocity. It's not unusual for this custom AI component to change the max speed and

acceleration as it reaches goals etc.

Code

NavMeshAgent agent = ...

// Sets the target position for the agent. It will try to get there
// until you tell it to stop.
agent.MoveTo( targetPosition );

// Stop trying to get to the target position.
agent.Stop();

// The agent's actual velocity
var velocity = agent.Velocity;

Create d 2 Fe b 2024

Updated 23 O ct 2025 about

Costs & Filters

Areas can be used:

to mark a section as more costly to traverse than others (e.g. shallow water)

to prevent certain agents from entering a specific area

Nav Area impacting agent Pathing behavior

Costs

Agent preferring the cheap area (green) over the expensive area (orange).

By default an agent can traverse any area.

But, you can also specify which areas an agent is allowed to travers and which not.

Maze made of Forbidden areas, one agent can take shortcuts in the maze.

Shortcutter Agent

Create d 22 O ct 2025

Updated 23 O ct 2025 about

NavMesh Areas

NavNesh Areas can affect NavNesh generation and agent behavior/pathing.

The NavMeshArea component is used to define the location, shape and type of an area.

You can also specify the Area for a link component.

Limitations

Currently there is a limit of 24 NavMeshAreaDefinition, but you can assign them to as many Area

Components as you like

Static areas are basically free.

Moving areas are a bit more expensive, but you should beable to have at least a couple of dozens

of them.

Create d 3 De c 2024

Updated 29 O ct 2025 about

Obstacles

Areas can be used to block of certain areas of the NavNesh both in editor and at runtime. This will

completely omit an area from navmesh generation.

Obstacles can be created by creating a NavMesh Area Component, enabling the IsBlocker flag.

Examples

Updated 29 O ct 2025 about

NavMesh Links

Creating Links

You can create links by adding a NavMeshLink Component to an GameObject.

Agent Link Traversal

Def ault T raversal

By default agents will linearly interpolate between start/end locations to travers the links.

about agent traversal.

Custom NavMeshLinkComponent:

public sealed class CustomLink : NavMeshLink

protected virtual void OnLinkEntered( NavMeshAgent agent )

protected virtual void OnLinkExited( NavMeshAgent agent )

NavMeshLink & NavMeshAgent Events:

public class NavMeshLink
 public Action<NavMeshAgent> LinkEntered;
 public Action<NavMeshAgent> LinkExited;

public class NavMeshAgent
 public Action LinkEnter;
 public Action LinkExit;

Custom Links

In most cases the default traversal wont suffice. You will likely want to move the game object from start to

end differently depending on the link that is being traversed.
If you want to handle the traversal yourself you first need to disable the default traversal on the agent. 

Agent.AutoTraverseLinks = false;

Afterwards there are couple options to take over the link traversal and handle it yourself:

1. By Overriding virtual void NavMeshLink.LinkEntered()

2. By subscribing to the Action<NavMeshAgent> NavMeshLink.LinkEntered event

3. By subscribing to the Action NavMeshAgent.LinkEnter event

4. Constantly checking for bool NavMeshAgent.IsTraversingLink in an OnUpdate method

In some cases you will want the link to handle the traversal, in others you may want to handle it on the

agent.

Regardless, of which you choose, after the traversal is finished make sure to call

NavMeshAgent.CompleteLink() to continue the regular agent navigation.

In the following we provide a few examples for custom traversal, that can be modified to your needs.

Basic Jump

Agent.CurrentLinkTraversal provides information about the link an agent is currently traversing.

The positional values can be used to drive custom movement and animations.

public Vector3 LinkEnterPosition;

public Vector3 LinkExitPosition;

public Vector3 AgentInitialPosition;

public NavMeshLink LinkComponent;

In this example we crate a custom link component that overrides OnLinkEntered . The component then

drives a simple parabolic jump for the agent using the data from Agent.CurrentLinkTraversal .

Note, how we manually update the Agents position every frame using Agent.SetAgentPosition() .

public sealed class JumpLink : NavMeshLink
 protected override void OnLinkEntered( NavMeshAgent agent )

ParabolicJump( agent );

 private async void ParabolicJump( NavMeshAgent agent )

var start = agent.CurrentLinkTraversal.Value.AgentInitialPosition;
var end = agent.CurrentLinkTraversal.Value.LinkExitPosition;

// Calculate peak height for the parabolic arc
var heightDifference = end.z - start.z;
var peakHeight = MathF.Abs( heightDifference ) + 25f;

var mid = (start + end) / 2f;

// Estimate prabolic duration size using a triangle /\ between start, mid, end
var startToMid = mid.WithZ( peakHeight ) - start;
var midToEnd = end - mid.WithZ( peakHeight );
var duration = ( startToMid + midToEnd ).Length / agent.MaxSpeed;
duration = MathF.Max( 0.75f, duration ); // Ensure minimum duration

TimeSince timeSinceStart = 0;

while ( timeSinceStart < duration )

var t = timeSinceStart / duration;

// Linearly interpolate XY positions
var newPosition = Vector3.Lerp( start, end, t );

// Apply parabolic curve to Z position using a quadratic function
var yOffset = 4f * peakHeight * t * (1f - t);
newPosition.z = MathX.Lerp( start.z, end.z, t ) + yOffset;

agent.SetAgentPosition( newPosition );

await Task.Frame();

agent.SetAgentPosition( end );
agent.CompleteLinkTraversal();

Ladders

Ladders follow a similar pattern. But the animated movement is different, it's divided into 3 parts:

1. Align with bottom of the ladder

2. Vertical Movement only to reach the ladder top

3. Walk off the ladder

public sealed class LadderLink : NavMeshLink
 protected override void OnLinkEntered( NavMeshAgent agent )

ClimbLadder( agent );

 private async void ClimbLadder( NavMeshAgent agent )

var initialPos = agent.CurrentLinkTraversal.Value.AgentInitialPosition;

var start = agent.CurrentLinkTraversal.Value.LinkEnterPosition;
var endVertical = start.WithZ( agent.CurrentLinkTraversal.Value.LinkExitPositi
var end = agent.CurrentLinkTraversal.Value.LinkExitPosition;

var climbSpeed = 100f;

var startDuration = (start - initialPos).Length / climbSpeed;
var climbDuration = (endVertical - start).Length / climbSpeed;
var endDuration = (end - endVertical).Length / climbSpeed;

var totalLadderTime = startDuration + climbDuration + endDuration;

TimeSince timeSinceStart = 0;

while ( timeSinceStart < totalLadderTime )

Vector3 newPosition = start;

// 1. Make sure we are positioned at the link start
if ( timeSinceStart < startDuration )

newPosition = Vector3.Lerp( initialPos, start, timeSinceStart / startD

// 2. Vertical Movement
else if ( timeSinceStart < startDuration + climbDuration )

newPosition = Vector3.Lerp( start, endVertical, (timeSinceStart - star

// 3. Move off ladder to link end position
else

newPosition = Vector3.Lerp( endVertical, end, (timeSinceStart - startD

agent.SetAgentPosition( newPosition );

await Task.Frame();

agent.SetAgentPosition( end );

agent.CompleteLinkTraversal();

Physics Based Jump

You can also let the physics system drive the jump for you.

For this one we will switch it up and implement the traversal on the agent rather than the link.

We create a new component that we will attach to the GameObject our NavMeshAgent is on.

In addition, we will also need a RigidBody and Collider.

To perform a jump we simply apply a velocity to the RigidBody.

Physics jumps are usually hard to get right consistently, because they can fail in the same way a player

jump can fail.

For example, jump was initiated to early/late or the jump was blocked by something mid air.

public sealed class NavigationLinkTraversal : Component

[RequireComponent]
NavMeshAgent Agent { get; set; }

[RequireComponent]
Rigidbody Body { get; set; }

[RequireComponent]
public SkinnedModelRenderer Model { get; set; }

protected override void OnEnabled()

Agent.AutoTraverseLinks = false;
Agent.LinkEnter += OnNavLinkEnter;

protected override void OnDisabled()

Agent.LinkEnter -= OnNavLinkEnter;

private void OnNavLinkEnter()

PhysicsJump();

private async void PhysicsJump()

Model.Set( "b_grounded", false );
Model.Set( "b_jump", true );

// Physiscs will drive our jump so disable game object position sync
Agent.UpdatePosition = false;

var start = Agent.CurrentLinkTraversal.Value.AgentInitialPosition;
var end = Agent.CurrentLinkTraversal.Value.LinkExitPosition;

var xyVelocity = Agent.MaxSpeed * (end.WithZ( 0 ) - start.WithZ( 0 )).Normal *

var velocity = xyVelocity + Vector3.Up * Math.Max( 500f, (end.z - start.z) * 8
// Launch the agent into the air
Body.Velocity = velocity;

TimeSince timeSinceStart = 0;

while ( true )

Agent.SetAgentPosition( WorldPosition );

var tr = Scene.Trace.Ray( WorldPosition + Vector3.Up * 0.1f, WorldPosition

.IgnoreGameObjectHierarchy( GameObject )
.Run();

if ( tr.Hit && timeSinceStart > 0.5f && tr.Distance < 4f )

break;

await Task.Frame();

Agent.SetAgentPosition( WorldPosition );

// Hand back position control to the agent
Agent.UpdatePosition = true;

Model.Set( "b_grounded", true );
Model.Set( "b_jump", false );

Agent.CompleteLinkTraversal();

Full Example on t est bed

You can find a full example that implements those 3 traversal types in our testbed:

https://github.com/Facepunch/sbox-

scenestaging/blob/main/Code/ExampleComponents/NavigationT argetWanderer.cs

Create d 3 Mar 2025

Updated 14 Apr 2025 about

Creating Terrain

To add T errain to your Scene, right click in the Hierarchy and select 3D Object → T errain from the menu.

The T errain inspector will then prompt you to create, import or link an existing T errain asset.

Create New T errain

Once you've created a T errain GameObject it will be blank, you need to create the T errain asset which

storesall the height maps, control maps, materials, etc. It can then be reused across multiple scenes.

In the inspector window with the T errain GameObject selected you will be asked how large you want your

terrain to be. Pressing Create New Terrain will prompt you where to save your terrain asset.

H e ig h t m a p

S iz e

The s iz e o f yo ur he ig ht ma p . H ig he r va lue s inc r e a s e VR A M us a g e

d r a s t ic a lly f o r c o mb ine d he ig ht ma p a nd c o nt r o l ma p s : 2 0 4 8 x 2 0 4 8 =

2 4 MB 4 0 9 6 x 4 0 9 6 = 9 6 MB 819 2 x 819 2 = 384 MB

World Scale

reduction of overall size.<br>A larger scale gives more overall size at the reduction of

How many inches per heightmap texel.A smaller scale gives more precision at the

precision.39 inches ~= 1 meter is a good default

Max Height

The maximum height your terrain will be in inches.The higher this is the less precision you

get at lower values.

If you already have a terrain created in one scene that you want to reuse you can either drag the terrain

asset in to automatically create the object, or press link existing and select an existing T errain asset.

Create d 18 Jul 2024

Updated 19 Jul 2024 about

Terrain

The T errain System allows you to create expansive outdoor environments quickly and easily in your scenes.

The pages in this section explain how to get started andall the various built-in options for T errain and how

to use them.

The T errain System is a work in progress, here's what is supported and what's not right now.

F e a t ur e Na me

S up p o r t e d

No t

S up p o r t e d

No t e s

Real-time editing

Import Heightmaps ✅

Level of Detail

Multi-Layer PBR

Materials

Material Height

Blending

Material Anti-Tiling

Physics Materials

Foliage

Trees

Basic sculpting tools & 2 layer texture painting

Import from World Machine, GeoGen, Gaia.

Anything that can export a 16 bit heightmap.

Very large landscapes possible

Support up to 32 materials.<br>Can import multiple

splatmaps.

Physics properties are applied per material used:

footstep sounds, bounciness, etc.

Grass & scatter meshes

S up p o r t e d

No t

S up p o r t e d

No t e s

Holes

Nav Mesh

Displacement

Create d 18 Jul 2024

Updated 11 Mar 2026

Vertex displacement about

Terrain Materials

A T errain Material is an Asset that defines a set of PBR textures, physics surfaces, detail meshes and

other properties that the T errain uses to render.

Because they are Assets you can easily reuse them on multiple T errains in different Scenes easily, transfer

them between projects, or use them from the cloud.

These are similar but different to standard Materials because T errain uses specialized shaders for rendering

to deliver performant landscape rendering with LOD support and material blending.

The first T errain Material you apply to a T errain automatically becomes the base layer, and spreads over

the whole landscape. You can then paint areas with other T errain Materials blending them together.

Creating T errain Materials

To create a new T errain Material, select your T errain GameObject and look at the Inspector, under T errain

Materials press New Terrain Material… Pick a save location and it will be automatically added to your

T errain Material list.

You can also create a T errain Material that isn't automatically associated with a T errain, by rick-clicking the

Asset Browser and selecting New Asset → New T errain Material…

Adding T errain Materials

Existing T errain Material assets can be dragged from the Asset Browser into the T errain Material list - or

onto the T errain itself.

T errain Materials can be found on the cloud by clicking the Browse… button, or filtering @cloud ext:tmat .

T here is a limit of 4 T errain Materials currently, this is planned to be resolved.

T errain Material Properties

Painting T errain Materials

The first material is applied across the entire T errain by default. You can paint subsequent T errain Materials

using the Paint T exture tool and selecting the T errain Material in the list in the inspector.

Updated 21 Jul 2024 about

VR

Enabling VR

Editor: Launch the editor with a headset connected. You'll see a VR button at the top right of your editor. It

should be on by default.

Game: If you have a VR headset plugged in and it's active, you'll launch in VR.

Components

VR Anchor: locks the player's playspace to a GameObject's transform

VR T racked Object: moves a GameObject's transform to a tracked device, e.g. a controller or

headset

VR Hand: matches the animgraph for a hand model with SteamVR's skeletal inputs

Example Setup

An example setup is available on sbox-scenestaging under the "test.vr" scene.

Here's a basic explanation of the different parts you'll come across:

Anchor

The anchor represents the center of the player's playspace.

If you want your player to beable to move around, add the "VR Anchor" component to the same

GameObject that you're using for your player. This will move the virtual playspace along with it.

Camera

Rendering

Left and Right eye targets in order to display properly inside the headset.

Tracking

A basic VR setup should also have a VR T racked Object component on the camera, set up with the Head

pose source, in order for the camera to follow the player's head movements.

Input

Tracking

On any object you want to track the player's controllers, add a VR T racked Component for the object you

want to track.

For example, this component will make the GameObject it's attached to follow the player's left controller:

API

Here's a basic overview of the VR C# API:

Input

Get controller values

var grip = Input.VR.LeftHand.Grip.Value;

// Check if the player is pulling the trigger a bit
if ( Input.VR.LeftHand.Trigger.Value > 0.5f )
 Log.Trace( "Shoot!" );

 // Vibrate the controller
 Input.VR.LeftHand.TriggerHapticVibration( duration: 0.5f, frequency: 10, amplitude:

Check if the player is running in VR

if ( Game.IsRunningInVR )
 Log.Info( "I am running the game in VR!" );

Create d 29 Jan 2024

Updated 16 Mar 2026 about

Explore the Engine

S&box uses a scene system to create games. We feel this is the easiest system for people to pick up, while

still being powerful.

The Scene System

Scenes

A Scene is your game world. Everything that renders and updates in your game at one time should be in a

scene. Scenes can be saved and loaded to disk.

GameObject s

A scene contains multiple GameObjects. The GameObject is a world object which has a position, rotation

and scale. They can be arranged in a hierarchy, so that children GameObjects move relative to their

parents.

Component s

GameObjects can contain Components. A component provides modular functionality to a GameObject.

For example, a GameObject might have a ModelRender component - which would render a model. It might

also have a BoxCollider component - which would make it solid.

The game developer ultimately creates games by programming new Components and configuring scenes

with GameObjects and Components.

Play T estbed

certain engine features, to make sure they work and keep working.

When you enter the game you'll find a menu of scenes. Each scene tests a different engine feature.

Click a scene to enter it, have a play around, press escape to return to the main menu. You can hold

escape to completely leave any game.

So here's what you just saw. The menu uses our UI system, which is like HT ML with C# inside. It's

basically Blazor, if you've ever heard of that.

When you clicked on a title, you entered a Scene. Our engine is Scene based, rather than map

based like the regular Source Engine. Scenes are json files on disk, and are very fast to load and

switch between - just like you experienced.

You probably saw a bunch of cool stuff. Here's something else cool — you can download the

source for that game here, which includesall the scenes. Once you download it just open the

.sbproj file to open it in the s&box editor, then explore the different scenes in the Asset Browser.

You can edit the scenes and play with them locally to get a feel of how things work.

Next Steps

Now that you understand the basics, explore these areas of the documentation:

Scenes & GameObjects — Deep dive into the scene system

Code — C# programming in s&box

Editor — Learn the editor tools

Gameplay — Input, navigation, terrain, and VR

Networking — Multiplayer, RPCs, and dedicated servers

Graphics — Shaders, effects, and post-processing

Updated 9 Apr 2026 about

FAQ

How do I get it?

We'll be releasing s&box on Steam on the 28th April for $20.

Access to the developer preview is now closed — you may or may not get to keep it post release

depending on play time, development or skins purchased.

Are you using workshop?

No. We've made a system where you don't have to install addons. This is what sbox.game is. In the same

way, you don't have to install videos from YouT ube; you just download what you need.

Why not Unity? Why not UE?

We're sentimental about the Source engine. Source 2 has a beautiful renderer and brings the engine up to

date with tools like ModelDoc and Animgraph.

It would have been cheaper and easier to do thisall on Unity or UE, but we would have loved it less.

Will creators beable to monetize?

Yes. It's integral. We owe our entire business to the fact that Valve let us monetize.

Right now there are two ways for our creators to make money. You can make a cosmetic item, which then

goes for sale in game and you get a cut of it via Steam Workshop. Or you can make a game and get a cut

of the playfund.

We want to be careful about pushing further. We want you to beable to charge for whatever you want,

but we also don't want everything to become pay-to-win like on other platforms.

So is it an engine, or a platf orm?

It's everything. An explanation was posted on this blog here.

Create d 13 Fe b 2024

Updated 5 Se p 2025 about

Your First Project

The best way to learn is to do. Open the s&box editor and on the welcome screen, choose New Project.

Create a Game - Empty project.

Creating Game Objects

Once open you have an empty scene. You can experiment by creating GameObjects by right clicking the

tree on the left, and selecting an object type to create.

Creating Components

After that, try to make a GameObject that you can control by creating a custom component by

selecting Add Component on the GameObject inspector and typing in a name. The file should open in

Visual Studio.

Player Input

Use the Input section of this site to figure out how to read keys, and change the WorldPosition depending

on which keys are being pressed.

the position directly using Scene.Camera.WorldPosition .

Congratulations - you just learned the basics of GameObjects and Components. You're a

game developer now.

Create d 9 Apr 2026

Updated 9 Apr 2026 about

Download & Install

The s&box editor and game are available to everyone through the developer preview.

Install

To install s&box click here or:

1. Open Steam

2. Click on the Library tab

3. Search for s&box

4. Install both the game and the editor apps

Launch

You can launch s&box in several ways:

Launch through Steam directly

Use a shortcut to sbox-dev.exe

Open your .sbproj file directly

Updated 9 Apr 2026 about

Getting Started

S&box is coded in C#. Under the hood, it uses the Source 2 engine (CS2, HL:Alyx, DOT A2) and some of its

systems: rendering, resources, physics, and audio.

We use a scene system, similar to Godot and Unity. This allows faster iteration, without everything being

code-based. The scene system aims to make how everything works more transparent, by being easily

visible, and easily accessible.

We have developed a hotload system which is capable of compiling & hotloading your changes to code

within a few milliseconds, which negates the need for a scripting language.

Our intention is to let you export the things that you make in our engine and release them standalone.

We'll let you do this royalty-free.

Download & Install

Get the s&box editor through Steam and start building. Available to everyone through the developer

preview.

System Requirements

Minimum and recommended hardware specs to run s&box.

Your First Project

Create a new game project, add GameObjects and Components, and get something moving on screen.

Explore the Engine

Understand the scene system, play the T estbed to see engine features in action, and find sample projects

to learn from.

Project T ypes

Learn about the different project types: game projects and addon projects.

Monetization

Learn how creators can make money through the Play Fund and other revenue systems.

Reporting Issues

FAQ

Answers to frequently asked questions about s&box.

Feature Status

Current status of key features and known missing functionality.

Community

If you don't understand something, please ask on the forums or on Discord in the beginner's channel.

Issues and feature suggestions should be posted in the sbox-public repo.

Create d 15 Jun 2025

Updated 9 Apr 2026 about

Monetization

An important part of s&box being a modern game platform is allowing the developers that use it to make

money from it.

Our plans around monetization are evolving over time, nothing is set in stone. We want to give

developersall the opportunities to make money possible without harming player experience.

The Play Fund

Every day we create a pool of money. That pool is distributed among the games and maps with the most

players.

What is it , like most players? Most hours?

It's based roughly on clamped individual player hours. The exact algorithm we use is kept secret. We will

need tweak the algorithm over time to encourage and discourage specific behaviours.

How do I enable it ?

Open your map or game package on sbox.game and go to Configure > Edit Features . You'll then see an

option to include it.

How do I know how much money I made?

The daily estimates are visible on your Organization's Page, under Monetization .

If you're using copyrighted material in your package - then no. If you're repackaging someone else's work

with no real creativity of your own, then no.

If you're using stuff from sbox.game where author permission is implicit, stuff you created, stuff with an

open license, then yes.

When are payment s made?

Payments are made towards the middle of every month, for the previous month. For example, in the

middle of March we'll pay out what you made in February.

You will need to have at least $100 pending to receive a payment. You also need to have set up your

payment information in your profile settings.

Can I subdivide payment s t o my t eam?

Yes! You can split your payments between your different team members.

They don't need to be members of the organization.

Is it just maps and games?

Yes, for now. It would be awesome for a map creator to beable to say "okay I used these models so I'm

gonna give this org 10%", but if we do that it's something that will come later. This is the first step.

Where's t he pool from? How much is it ?

I'd like to get more transparent about the pool in the future and show the figure somewhere. For now, while

we're finding out feet, it's not public.

Garry's Mod's revenue is funding the development of s&box. So the fund is from Garry's Mod for now. Our

hope is that one day s&box will beable to stand on its own two feet, and the fund will grow with its success.

Updated 15 Jun 2025 about

Project Types

When creating a new project in s&box you are presented with a few different project types to make.

The sbproj f ile

The .sbproj file holds your project's information like its title and type. It tells s&box that this is a project

folder.

Create d 3 O ct 2024

Updated 15 Jun 2025 about

Reporting Errors

Errors will happen. Here's how to make a useful error report.

Issue Tracker

We use github to track issues. Our issue repository is here. When issues are submitted, they're triaged and

assigned priorities on our project here.

Error Logs

It's often really helpful to us to have your log to work out what's going on. If you get any errors, these will be

printed in the log file along with their stack trace, and any other messages.

They're written to the logs folder inside your s&box installation directory, the quickest way to get to this is

by right-clicking s&box in Steam.

this to your issue on GitHub.

An error message on its own is usually not very useful. If you can provide a stack trace too, by

either uploading the log or copy/pasting from the console (by clicking the error in the in-game

console), it'll make things much easier to diagnose.

Please don't upload screenshots of the console, they aren't useful.

Hard Crashes

When you get a hard crash (the game or editor exits on its own) then the crash log is generally

automatically generated and uploaded to our backend.

While these crash logs are useful in revealing the problem, sometimes it's not obvious. If you have found a

way to reproduce the crash, that's really useful, please make an issue. If the crash needs a specific asset to

cause the crash, please provide that too.

Finally, please provide your 64-bit steamid (steamID64); this lets us look up your crash dumps very easily.

You can use websites like these to find it.

Common Errors

You NEED the following, if you don't have the following this is likely why:

At least 4GB of RAM, 8GB for the editor.

A graphics card that isn't older than 12 years

St eam Not Found

This tends to happen when you've got a Steam emulator on your system from pirating games, naughty.

Failed t o init ialize Vulkan

Graphics cards have supported Vulkan since 2012. If you don't have one, get one.

If you are on a laptop, make sure your drivers are up to date for your integrated and dedicated graphics.

Prot on Errors

If something is working on Windows but doesn't work on Proton, tell the Proton team

https://github.com/ValveSoftware/Proton/issues/4940

Create d 18 Jan 2024

Updated 15 Jun 2025 about

Status

As you play with developing in s&box, you will notice some things are weird, missing, or suck. We are aware.

Here's the current status of key features and missing functionality you'll run into.

Na me

Audio

Multiplayer

UI

D e s c r ip t io n

🟢 Can play sounds, music, voice chat, can play them positionally or 2D<br />🟢 Audio
processing, effects system<br />🟢 Lip sync<br />🟠 No auto voice ducking

🟢 Can create server, join server, sync vars, gameobjects, rpcs<br />🟢 Dedicated server
support<br />🟠 No error handling, permissions

🟢 Razor and Panel class UI, full style sheets, transitions, transforms, animation, world

panels

Scenes

🟢 Can create scene, gameobject, components, play, stop

Controller

🟢 Controller input<br />🟠 UI navigation with virtual cursor, missing element navigation, on-

screen keyboard

Navigation

🟢 Recast navmesh, agents, pathfinding, links

Platforms

🟢 Windows<br />🟠 Is likely to expand in the future, just not a priority

Hammer/Maps

VR

Particles

🟢 Create + Load maps, brushwork, props, lights, select + launch map in game<br />🟢 Can

use GameObjects

🟢 Easy to develop for, built-in components<br />🟠 Accessibility, user experience needs

work, needs more testing

🟢 Create particle effects, emitters, sprite rendering, model rendering, trails, lights, velocity,
collision<br />🟢 Totally moddable and extendable<br />🟠 No built in line renderer, motion

vectors, normals

Standalone

🟠 Working on export to standalone version license. Exporter works.

Physics

Editor

2D

🟢 Full 3D and 2D physics, great performance + stability

🟢 Scene editor, editor tools, inspector, editor apps, key re-binding

🟢 2D physics, ortho camera<br />🟠 Basic sprite support<br />🔴 No 2d editor mode

D e s c r ip t io n

GameResources

🟢 Custom game resource types, with inspector editing<br />🟠 No binary writing support

yet

Terrain

🟠 Early development, basic editing<br />🔴 No grass/detail models yet

Animation

🟢 Valve's animgraph system, events, IK, animated ragdolls, morphs<br />🟠 Some

advanced features currently rely on an undocumented format

PostProcessing

🟢 Shader support, camera-based post-process base component

Create d 19 Jan 2024

Updated 15 Jun 2025about gamesgames business_centerworkshop forumforum docsdocs Find Docs..ERROR: Cleaning too aggressive for this file.

s&

 about

games games

business_center workshop

forum forum

docs docs

Find Docs..

 s&box

 Documentation

S&box Documentation

About

S&box is coded in C#. Under the hood, it uses the Source 2 engine (CS2, HL:Alyx, DOT A2) and some of its

systems: rendering, resources, physics, and audio.

When you create games and addons in s&box, you will be creating them in C#.

We have developed a hotload system which is capable of compiling & hotloading your changes to code

within a few milliseconds, which negates the need for a scripting language.

Scenes

We use a scene system, similar to Godot and Unity. This allows faster iteration, without everything being

code-based. The scene system aims to make how everything works more transparent, by being easily

visible, and easily accessible.

Future

Our intention is to let you export the things that you make in our engine and release them standalone.

We'll let you do this royalty-free.

Reporting Issues

Issues and feature suggestions should be posted in the sbox-public repo.

Please see Reporting Errors.

Getting Started

Please see First Steps.



>Getting StartedSceneCodeEditorExporting StandaloneAssetsRenderingNetworking & MultiplayerPhysicsUIGame MountsActionGraphMovie MakerMediaSoundGameplayServicesAnimation🚀🪑💼🔩🧍🎎🎨🧑‍🤝‍🧑⚡🖥🎮🍝🎬💿🔊🎮💽🕺News Docs Metrics

FAQ Forum Discord Twitter



Getting StartedSceneCodeEditorExporting StandaloneAssetsRenderingNetworking & MultiplayerPhysicsUIGame MountsActionGraphMovie MakerMediaSoundGameplayServicesAnimation🚀🪑💼🔩🧍🎎🎨🧑‍🤝‍🧑⚡🖥🎮🍝🎬💿🔊🎮💽🕺
about gamesgames business_centerworkshop forumforum docsdocs Find Docs..about gamesgames business_centerworkshop forumforum docsdocs Find Docs..about gamesgames business_centerworkshop forumforum docsdocs Find Docs.. about

Editor Map

Toolbar

Project

File Menu

Create, open, or import movies.

Movie Player Selection

Select a or create a movie player in the current scene.

Hist ory

T oggle a panel to show modification history, so you can undo / redo changes.

Playback

T oggle recording changes from the scene into the timeline.

Play / Pause

T oggle playback of your movie.

Repeat

T oggle looping for when playback reaches the end of the movie.

Playback Speed

Controls both playback and recording rate.

Sync Movie Players

T oggle synchronizingall movie players in the scene when previewing playback.

Edit Modes

Keyframe Edit or

Switch to the keyframe editor mode, for simpler animations. Find out more here.

Motion Edit or

Switch to the motion editor mode, for finer control than keyframe editing. Find out more here.

Snapping

Object Snap

Snap to objects in the timeline when dragging.

Frame Snap

Snap to the current frame rate when dragging.

Frame Rat e

Resolution to use when frame snapping.

Track List

Parent Movie

Name of the outer movie, when editing a sequence.

Current Movie

Name of the currently opened movie resource.

Sequence St art / End

Block of time referenced by an outer movie, when editing a sequence.

T rack T ypes

Game Object Track

Gets bound to an object in the scene to be controlled during playback. Contains component and property

tracks.

Component Track

Gets bound to a component in the scene, defaults to a matching component of the parent game object

track. Contains property tracks.

Propert y Track

Named property within the parent track, describes how that property should change over time. Can

contain nested property tracks.

Sequence Track

Contains time blocks from another movie, making it easier to organize and edit complex projects. 

Expand / Collapse

Show or hide nested tracks.

Lock / Unlock

T oggle lock state of a track.

Select ed Track

Selecting a track will show relevant gizmos in the scene view.

Locked Track

Disables modifications of this track in the movie.

Timeline

Shif t - smoothly preview the time under the mouse

Scroll - vertically scroll through track list

Shif t+Scroll or Middle-Click+Drag - pan horizontally

Ctrl+Scroll - zoom in / out

Alt+Scroll - scrub forwards / backwards by a frame

Regions

Scrub Bar

Displays time labels. Click and drag to move the playhead.

Tracks

Describe how properties change over time. Edited in either the keyframe or motion editor.

Sequence Block

References a time block from another movie, nested in this one.

Start and end time of the currently edited sequence block, nested in another movie.

Markers

Playhead Marker

Currently selected time for editing.

Preview Marker

Current time being previewed by holding shift and mousing over the timeline.

Frame Tick

Based on the current frame rate, frame snapping will snap to these.

Loop St art / End

T ime range to loop when previewing playback. Set with alt+click+drag on a scrub bar.

Create d 1 Jul 2025

Updated 4 Jul 2025 about

Exporting Video

The currently open movie can be exported to a video file using the Export Video.. option in the file menu.

This will open a window that lets you tweak the output path, resolution, format, and quality of the exported

video.

Camera Control

The video will be rendered from the perspective of any active camera in the scene. You should therefore

control camera motion using tracks in your movie project. You can also use tracks to toggle which

cameras are enabled in the scene, if necessary.

Motion Settings

When exporting, you can optionally enable motion smoothing at various strengths and quality levels. When

enabled, each final exported frame will be made out of many sub-frames with a very small time step

between them. This simulates having the camera's photosensor be exposed for a non-zero amount of

time for each frame.

This controls what fraction time for each frame the sensor is exposed for. Very Fast will expose the sensor

for 1/12th of a frame, Medium is ½, and Very Slow makes the sensor always exposed for very blurry motion.

Instant will disable motion smoothing.

Motion Qualit y

Use this to control how many sub-frames are rendered for every final output frame. This will greatly affect

how long it takes to render your project, so you can set this to Low when previewing an export to save a lot

of time.

Image Sequence / Atlas

You can also export individual images for each frame of your video, or a single atlas with a tile for each

frame. You can find these options in the Encoding tab.

Exported images can be JPEG or PNG, with PNG supporting transparent backgrounds.

The background will be transparent if you have no skybox, and the camera's clear colour has 0

alpha.

Create d 30 Se p 2025

Updated 30 O ct 2025 about

Getting Started

In this article you'll find out:

How to open the Movie Maker editor

What is a Movie Player

What is a Movie Resource

What is a T rack

Movie Editor

Opening the Movie Editor

If Movie Maker isn't already visible, you can toggle it in the View menu.

It should fit nicely as a tab in the lower panel if you dock it there.

Movie Player

To edit and preview movies, you'll need a Movie Player component somewhere in your scene. Movie Players

decide which objects in the scene should be animated by a particular movie, and control the current

playback position.

If you don't have any Movie Players in the current scene, you should see a big button to create one.

Otherwise, you can switch between players or create new ones by using the drop-down in Movie Maker's

menu bar. This will only list players in the currently active scene.

You can also add one to a GameObject in the Inspector like any other Component.

Movie Resources

Movies can either be embedded inside a Movie Player, or saved as a .movie asset.

Saving & Loading

New movies will be embedded in the current Movie Player by default. You can save them as reusable

.movie files, or embed a copy of the currently edited .movie, with the File menu.

You can also reference segments of movies from each other using sequence blocks. This can be done by

selecting Import Movie in either the file menu or when right-clicking in the timeline.

Tracks

Movies describe how properties in a scene should change over time, and this information is stored in tracks.

T here's a few types of track you'll need to know about.

Reference Track

This track references a GameObject or Component in the scene that should be controlled. It's up to the

Movie Player to decide which particular object to bind each track to, so you can re-use the same .movie to

control different actors.

Propert y Track

This represents a property somewhere in the scene, and describes how it should animate. This could be the

position of the camera, the colour of a light, or text in a speech bubble.

Property tracks are always nested inside other tracks, either reference tracks or other properties. This is

how the track knows what to control in the scene: it checks what the parent track is bound to, and looks up

a property inside it with the track's name.

Sequence Track

This track references blocks of time from another movie, helping you organize and edit bigger movie

projects with multiple shots.

Creating T racks

Reference and property tracks can be created by dragging from the hierarchy or inspector into the track

list.

You can also create sub-tracks by right-clicking an existing track, and selecting the tracks you want from

the context menu.

timeline, or through the file menu.

Next Steps

Editor Map - find your way around the movie editor

Keyframe Editing - a great place to start making simple animations

Motion Editing - make more detailed animations and edit recordings

Recording - manually puppet characters or record gameplay

Sequences - cleanly structure big projects with nested movies

Playback API - define movies and play them back using C#.

Recording API - record and save the gameplay using C#

Updated 27 Aug 2025 about

Keyframe Editing

This is the simplest way to describe how stuff in your scene should animate. Create keyframes in property

tracks that are snapshots for what values that track should have at specific times, then control how the

track should blend between those values.

It will be active by default, but you can toggle it with the key-shaped button in the toolbar.

Creating Keyf rames

T here's three ways to create a keyframe for a property track:

Change the property that the track is bound to, a keyframe is created at the current playhead time

Right-click on the track in the timeline, and select Create Keyframe in the context menu

T oggle Create Keyframe on Click either by holding Shift or pressing the button in the toolbar, then

clicking in the timeline

Copy the scene view's perspective into a selected camera with Ctrl+Shift+F

Interpolation Mode

Each keyframe can choose between three different interpolation modes:

Linear - change at a constant velocity

Quadratic - ease in / out, with 0 velocity at the keyframe

Cubic - move along a smooth spline connecting keyframes

You can combine different modes for neighbouring keyframes to make animations ease in or out.

Automatic T rack Creation

For convenience, you can enable this mode to create tracks whenever you touch something in the scene.

This helps the most when you're changing lots of properties on many objects, so you don't have to

manually created dozens of tracks.

Updated 3 Jul 2025 about

Movie Maker

Movie Maker is a timeline-based editor built into S&box for animating anything in your scene. Keyframe

object properties, record gameplay, animate characters with bones and IK, and export finished videos — all

without leaving the editor.

What Can You Make?

Cutscenes — choreograph cameras, characters, and events on a timeline

T railers & Videos — compose shots and export directly to video

Skeletal Animation — pose and animate skinned characters with bones, IK, and motion editing

T imed Events — synchronize lights, audio, UI, and gameplay triggers

Recorded Gameplay — capture live gameplay and refine it into polished animation

How It Works

A Movie Player component in your scene controls playback of a Movie Resource, which contains tracks

describing how properties change over time. Drag any GameObject or property onto the timeline to start

animating it.

sequences to organize complex multi-shot projects.

Pages

🌱 Getting Started — set up your first movie and learn the basics
🗺 Editor Map — find your way around the interface
🔑 Keyframe Editing — animate properties with keyframes
🖌 Motion Editing — fine-tune animations with curves and layers
🦴 Skeletal Animation — animate characters with bones and IK
🎥 Recording — capture gameplay as animation data
🎞 Sequences — combine clips into multi-shot projects
📼 Exporting Video — render to video files
🧑‍💻 Playback API — play movies from code
🧑‍💻 Recording API — record animations programmatically

Create d 30 Jun 2025

Updated 19 Apr 2026 about

Motion Editing

This editor mode gives you finer control over track data. Instead of keyframes, you sculpt the raw track

data itself at any resolution you want.

To motion edit, you select a time range of one or more tracks, then tweak the properties that those tracks

represent to manipulate track data. You can also cut / copy / paste ranges of time, or save the selection

as a separate .movie file.

Time Range Selection

A time range selection describes how much a modification affects each moment in time. It's broken up

into three parts:

Fade In - modifications gradually ramp up within this range

Peak Range - times in this range are fully affected by modifications

Fade Out - modifications ramp down within this range

Click and drag in the timeline to select a time range

Hold Shift and scroll to increase / decrease the fade in / out time

Drag any of the parts of a time range to move or resize them

Use Ctrl+A to select the whole movie's duration

Press Esc to clear the selection

You can change the easing type of the fade in / out sections with the corresponding button in the toolbar,

or pressing number keys when mousing over those sections. The shape of the top / bottom of the time

selection UI shows what the current easing function looks like.

After selecting a time range, you can manipulate the properties of your movie's tracks. Only the selected

time range will be affected, with the changes ramping up and down inside the fade in / out sections of

your selection.

The selection will turn yellow to show a modification is in progress. At this point you can freely tweak the

time selection, and when you're happy hit Enter or click the green tick to commit the change.

Context Menu

The context menu for time selections has a ton of extra editing actions.

Insert (Tab) - add empty time inside the selected range, moving existing track data to the right

Remove (Backspace) - delete the selected range, moving everything afterwards to the left

Clear (Delete) - delete the selected range, leaving empty time

Save As Sequence.. - save the selected range to a .movie, and reference it in the current project

Clipboard Act ions

Cut (Ctrl+X) - copy the selected range to the clipboard, then clear the range

Copy (Ctrl+C) - copy the selected range to the clipboard

Paste (Ctrl+V) - paste previously copied track data as a modification

Additive Editing

When pasting a time selection, you can additively layer track data over the existing animation. This is

enabled by default, can can be disabled by clicking the Additive button in the toolbar while modifications

are active.

Updated 9 Jul 2025 about

Playback API

You can define movies and play them back using C#.

Tracks

T racks can represent a GameObject reference, a Component reference, or a property that should be

animated.

Create a reference track that, when played, binds to an object named "Camera".

using Sandbox.MovieMaker;

var objectTrack = MovieClip.RootGameObject( "Camera" );

Create a property track that binds to a property named "LocalPosition" inside of whatever objectTrack is

bound to.

Give it a constant value between 0s and 2s, then a different constant value from 2s to 5s. After 5s it has no

value.

var positionTrack = objectTrack
 .Property<Vector3>( "LocalPosition" )
 .WithConstant( timeRange: (0.0, 2.0), new Vector3( 100, 200, 300 ) )
 .WithConstant( timeRange: (2.0, 5.0), new Vector3( 200, 100, -800 ) );

Create a property track that binds to the "FieldOfView" property of a CameraComponent attached to

whatever objectTrack is bound to. Give it an array of samples between 1s-3s.

var fovTrack = objectTrack
 .Component<CameraComponent>()
 .Property<float>( "FieldOfView" )
 .WithSamples( timeRange: (1f, 3f), sampleRate: 2, [60f, 75f, 65f, 90f, 50f] );

Animate the scene with each track. They will try to bind to root objects in the scene with the matching

names and component types, and silently fail if they don't exist.

positionTrack.Update( time );

MovieClip

Group tracks into a clip so we can animate themall together.

var clip = MovieClip.FromTracks( positionTrack, fovTrack );

clip.Update( time );

You can search for tracks by path.

var camTrack = clip.GetReference( "Camera" );
var posTrack = clip.GetProperty<Vector3>( "Camera", "LocalPosition" );

Clips can be serialized to and from JSON.

Log.Info( Json.Serialize( clip ) );

TrackBinder

What does objectTrack bind to in the current scene?

var target = TrackBinder.Default.Get( objectTrack );

Log.Info( target.IsBound );
Log.Info( target.Value );

12:59:08 Generic True
12:59:08 Generic GameObject:Camera

Bind the track to something else.

target.Bind( Game.ActiveScene.Camera.GameObject );

Binders can be serialized too.

Log.Info( Json.Serialize( Binder.Default ) );

We can have multiple Binder instances, so the same clip can control different objects.

var binder = new TrackBinder( Game.ActiveScene );

binder.Get( cameraTrack ).Bind( Game.ActiveScene.Camera );

cameraTrack.Update( time );

// Using our own Binder instance

cameraTrack.Update( time, binder );

T arget Creation

By default, the player will create any GameObjects or

Hidden. You can turn this off

Components referenced by the recording that aren't already

NotNetworked

with the CreateTargets

in the scene. These targets will be flagged as NotSaved

property.

moviePlayer.CreateTargets = false;
moviePlayer.Play( clip );

You can also manually create targets through the player's TrackBinder.

// Create targets for every track in the given clip
moviePlayer.Binder.CreateTargets( clip );

// Create targets for a specific set of tracks
var track1 = clip.GetTrack( "Example", "ModelRenderer" );
var track2 = clip.GetTrack( "Player", "PlayerController" );

moviePlayer.Binder.CreateTargets( [track1, track2] );

MoviePlayer

The MoviePlayer component has a clip, a binder, and a time position.

var moviePlayer = GameObject.AddComponent<MoviePlayer>();

moviePlayer.Clip = clip;
moviePlayer.Binder.Get( clip.GetReference( "Camera" ) ).Bind( Game.ActiveScene.Camera

// Time in seconds

moviePlayer.Position = 0.75;

The clip can also be from a resource.

moviePlayer.Resource = ResourceLibrary.Get<MovieResource>( "example.movie" );

Updated 18 Mar 2026 about

Recording API

You can record gameplay into a MovieClip, which can be played back or imported into Movie Maker for

editing. This could be useful for killcams in shooters, leaderboard replays in racing games, or for capturing

gameplay to edit into a trailer.

This feature is provided by the MovieRecorder class. You can use its default behaviour to captureall

display-related components in the scene, or configure it to capture only certain objects, components and

properties.

Recording Basics

By default, a MovieRecorder will captureall Renderers, Cameras, SoundPoints and particle-related

components. Just create a recorder, and call Start.

// Create a recorder using the default capturing options
var recorder = new MovieRecorder( Scene );

// Start capturing
recorder.Start();

This starts capturing the scene every fixed update. When you want to stop recording, call Stop.

// Stop capturing
recorder.Stop();

You can then compile the recording into a MovieClip for playback in a MoviePlayer, or to save into a

MovieResource.

// Convert the recording to a MovieClip
var clip = recorder.ToClip();

// Play the clip!
GetComponent<MoviePlayer>().Play( clip );

// Save it to a .movie
FileSystem.Data.WriteJson( $"movies/example.movie", clip.ToResource() );

Manual Capture

Instead of Start and Stop, call Advance to move the recording along by an amount of time, and Capture to

record a frame.

while ( IsRecording )
 SimulateScene();

 // Move the recording time along by 10ms
 recorder.Advance( 0.01 );

 // Capture a frame
 recorder.Capture();

Configuring Recorders

If you want to be more selective about what gets recorded, create a MovieRecorderOptions instance and

pass it in to the MovieRecorder constructor. These options let you specify the sample rate, filter which

GameObjects are allowed to be captured, and add actions to run during each capture.

A new options instance won't capture anything, letting you fully configure it.

var options = new MovieRecorderOptions( SampleRate: 60 )
 .WithCaptureAll<Player>()
 .WithComponentCapturer<PlayerCapturer>()
 .WithCaptureAction( x => x
 .GetTrackRecorder( scoreManager )
 .Property( "Score" )
 .Capture() );

var recorder = new MovieRecorder( Scene, options );

Def ault Options

If you want to base your configuration off the default options (which capturesall renderers, cameras,

particles etc), you can access it through MovieRecorderOptions.Default.

var options = MovieRecorderOptions.Default with { SampleRate = 60 }
 .WithFilter( x => !x.Tags.Has( "effect" ) );

You can customize the default options by creating one or more static methods with a

[DefaultMovieRecorderOptions] attribute, like this:

[DefaultMovieRecorderOptions]
public static MovieRecorderOptions BuildDefaultOptions( MovieRecorderOptions options )

return options

.WithFilter( x => !x.Tags.Has( "viewmodel" ) )

.WithFilter( x => x.PrefabInstanceSource?.StartsWith( "prefabs/surface/" ) is

The default options will be used when pressing the Record button in the Movie Maker editor, and the

movie  console command in-game.

Sample Rate

By default, property tracks in the generated recording are resampled at 30 FPS to keep file sizes small. You

can choose a different rate when creating a MovieRecorderOptions, or use the with syntax on an existing

instance.

var options = new MovieRecorderOptions( SampleRate: 60 );

var options = MovieRecorderOptions.Default with { SampleRate = 60 };

Filters

Adding filters lets you control which GameObjects are allowed to be captured. Components won't be

recorded if their containing GameObject, or any of its ancestors, are filtered out. The first time a capture is

attempted on an object, it is checked againstall provided filters. If any return false, that object and any of

its descendants will be ignored during recording.

var options = MovieRecorderOptions.Default
 .WithFilter( x => !x.Tags.Has( "effect" ) )
 .WithFilter( x => !x.Name.StartsWith( "decal_" ) );

Capture Actions

Every time Capture is called on a MovieRecorder, it goes throughall the capture actions in its

MovieRecorderOptions. These actions will then access track recorders for GameObjects, Components, and

properties, then call Capture on them.

// Capture "ExampleProperty" from inside exampleComponent
var options = new MovieRecorderOptions()
 .WithCaptureAction( x => x
 .GetTrackRecorder( exampleComponent )
 .Property( "ExampleProperty" )
 .Capture() );

Component Capturers

Most of the time you'll want to capture specific properties fromall instances of a given component type.

To simplify this, you can implement ComponentCapturer<T>. Whenever Capture is called on a

component's track recorder, all component capturer instances that match that component's type will be

invoked.

protected override void OnCapture( IMovieTrackRecorder recorder, ModelRenderer com

recorder.Property( nameof( ModelRenderer.Model ) ).Capture();
recorder.Property( nameof( ModelRenderer.Tint ) ).Capture();
recorder.Property( nameof( ModelRenderer.MaterialOverride ) ).Capture();
recorder.Property( nameof( ModelRenderer.RenderType ) ).Capture();

if ( component.HasBodyGroups )

recorder.Property( nameof( ModelRenderer.BodyGroups ) ).Capture();

All capturers with public parameterless constructors will be included in MovieRecorderOptions.Default, or

you can manually add capturers to an options instance. These capturers are invoked when Capture is

called on a matching component's track recorder.

var options = new MovieRecorderOptions()
 .WithComponentCapturer( new ModelRendererCapturer() )
 .WithCaptureAction( recorder =>
 foreach ( var renderer in recorder.Scene.GetAllComponents<ModelRenderer>() )
 // This will look for matching ComponentCapturers
 recorder.GetTrackRecorder( renderer )?.Capture();

For convenience, WithCaptureAll does the same job as the above example capture action.

var options = new MovieRecorderOptions()
 .WithComponentCapturer( new ModelRendererCapturer() )
 .WithCaptureAll<ModelRenderer>();

Create d 4 Fe b 2026

Updated 18 Mar 2026 about

Recording

Capture gameplay or hand-puppet properties to quickly animate parts of your scene, then tweak the

recordings to polish everything up.

Recording in Play Mode

This lets you act out the roles of characters by controlling them directly in-game, be a camera operator

for a scene you've already animated, or capture gameplay for a trailer.

First create tracks for any properties you want to record. Common tracks will be added for you when

dragging certain objects into the track list, like Player Controllers.

After that, enter play mode and press the T oggle Record button. Any changes to properties bound to

tracks will get recorded directly to your movie. When you're done, hit the T oggle Record button again.

Your recording will still be in your movie when you exit play mode, letting you edit it further and save it.

Recording in Editor

for polishing later. As before, make sure you've created tracks for any properties you want to record, then

use the T oggle Record button to start and stop recording.

Editing

After making your recording, you can then polish it up in the Motion Editor or Keyframe Editor. Here's some

extra recording specific tips:

Cutting

Your best bet here is to save your recording to a separate .movie, then reference it as a sequence block in

your main project. This lets you take clips from the recording, tweaking the start and end times as needed.

Smoothing

Recordings can be shaky, especially when hand puppeting or manually operating a camera. Use the

Smoothen option in the Motion Editor context menu to round out any rough edges in a selected time

range. You can control how big the smoothing window is, with larger values leading to smoother tracks.

Updated 10 Jul 2025 about

Sequences

Sequence blocks are clips taken from other .movie assets. This helps you divide up big projects however

you like: individual scenes, or individual actors in each scene can be grouped into their own .movie files.

T here's no limit to how deep you nest your sequences.

Sequence blocks also give you a convenient way to edit your movie. You can move them around in the

timeline, or clip their start and end times without editing raw track data. Multiple sequence blocks can

reference the same source .movie, so you can edit down a long recording into just the action you need.

Creating Sequences

Any project saved as a .movie resource (in the file menu) can be used as a sequence.

If you want to split your existing movie into multiple sequences:

1. Switch to the Motion Editor

2. Select the time range you want to save as a sequence

3. Select Save As Sequence.. in the context menu

Both the file menu and timeline context menus have an Import Movie option. After selecting a movie, a

new sequence block will be created with the duration of the referenced clip.

Editing Sequence Blocks

Sequence blocks can be moved and resized with the mouse. Multi-selecting sequence blocks lets you

move them together, and if their starts or ends align you can drag those together too.

Double-clicking on a sequence block will start editing the referenced movie, with the sequence block's

time range highlighted in the timeline. The top of the track list will show you how the current project is

nested, and you can return to outer movies by clicking them there.

Splitting Sequence Blocks

This will give you two blocks, which you can move and resize as you wish.

Create d 30 Jun 2025

Updated 10 Jul 2025 about

Skeletal Animation

You can animate skinned characters directly in the editor using Movie Maker. This tutorial covers:

Enabling the skeletal animation tools

Importing animation sequences from a model

Generating bone animation track data using AnimGraph

Recording bone animations from gameplay

Upgrading legacy procedural bone object animations

Using IK to manipulate poses

Getting Started

Movie Maker's skeletal animation tools are enabled if you have at least one SkinnedModelRenderer in your

movie with a Bones sub-track. When enabled for a renderer, you'll see its skeleton.

You'll also need to be in the Motion Editor to do the modifications described in this tutorial.

Base Animations

Animating skinned objects from scratch can be time consuming, so you'll usually want to start with an

imported or generated base-level animation that you can tweak later.

Importing Animation Sequences

For simple sequences you can just load an animation from your model.

2. In the timeline, select a time range that you want to import an animation for

3. Right-click on a selected region of track that belongs to the object you want to animate

4. Select Import Anim Sequence, and pick a clip

5. Drag the imported sequence around or trim the start / end times

6. Click the green Apply button to save the modification

Root motion will be included by default, you can disable it by locking the LocalPosition /

LocalRotation tracks of the object you're animating.

Generating Using AnimGraph

You can save a lot of time by letting AnimGraph generate an animation for you. You'll just need

LocalPosition and LocalRotation tracks describing how your character moves. These can be created in any

way you like: keyframes, recording, or motion editing.

Rot at e Wit h Motion

If you've only got a LocalPosition track, you can generate a LocalRotation track that always looks in the

direction of movement. Just select the time range you want to generate rotations for in the motion editor,

then right-click and select Rotate with Motion in the context menu, and apply if you're happy with it.

character to side-step or walk backwards at any point.

Motion t o AnimGraph Paramet ers

When you have LocalPosition and LocalRotation tracks for your SkinnedModelRenderer, you can generate

AnimGraph parameter tracks based on that motion. Select the time range you want to generate the track

data for, and select Motion to AnimGraph Parameters in the context menu.

You can find the generated tracks nested under Parameters in the track list, and again they can be

tweaked using keyframes or motion editing before moving to the next step.

AnimGraph Paramet ers t o Bones

If you want to have more fine-grained control over how your character moves, you'll need to bake its

animation into bone tracks. As always, select the time range you want to bake, then select AnimGraph

Parameters to Bones in the context menu. Now you're ready to move on to the Manipulating Poses section.

Recording Gameplay

Another way to generate initial bone track data is to record it in play mode. You'll just need to create tracks

for the bones you want to record before you start. We've included a sub-track preset for the built-in player

controller as an example.

Before we had dedicated bone track support, the best you could do was to enable Create Bone Objects on

a SkinnedModelRenderer and addall the created objects to your movie. If you have an existing animation

using that method, you can upgrade it to the new-style bone tracks with this context menu option. After

doing the upgrade, you can manually delete the old tracks and disable Create Bone Objects.

Manipulating Poses

We have some basic tools to help you tweak how your characters are posed during your movie. This is fairly

minimal currently, but should be enough to do things like layer upper body motion on top of a walk

animation generated using the above methods.

You should know the basics of Motion Editing before getting started here.

Moving Bones

First, select a time region in your movie that you want to animate a pose change for. Next, click and drag

from a joint. We'll simulate an IK chain going from the dragged bone to the root to try to find a sensible

pose. While dragging, you can press Esc to cancel. Press the green Apply button when you're happy to

commit the change to your animation.

When dragging a bone, you can hold the E key to start rotating it in place.

Locking Bones

Bones can be locked or unlocked in the context menu, or by holding Shift and clicking on them. This can be

especially useful for things like finger posing by locking the hand.

Currently this will only animate correctly if you lock an ancestor of whichever bone you're

manipulating. You can lock descendant bones like in the example below, but the lock is only

considered for the current playhead time while posing.

Create d 17 Nov 2025

Updated 26 Nov 2025 about

Connection Permissions

The host can change some permissions for a specific Connection . The ideal place to set these

permissions would be in the OnActive network event.

Spawning Objects

You can set Connection.CanSpawnObjects to allow or disallow a specific connection to create their own

networked objects. By default this is true .

Refreshing Objects

By default only the host can send network refresh updates for networked objects. This can be changed to

allow the owner of a networked object to also send these updates with Connection.CanRefreshObjects .

Create d 21 Mar 2024

Updated 21 Mar 2024 about

Custom Snapshot Data

In some circumstances you may want to add additional data to the network snapshot that gets sent to

clients when they join a server. One example of this might be serializing and deserializing voxel world data.

Components in the Scene can write and read their own data during the snapshot sending and receiving

process by implementing Component.INetworkSnapshot .

Writing Snapshot Data

To write snapshot data for a Component you can simply override the WriteSnapshot method on a

component.

private byte[] MyVoxelData { get; set; }

void INetworkSnapshot.WriteSnapshot( ref ByteStream writer )

 writer.Write( MyVoxelData.Length );

writer.WriteArray( MyVoxelData );

Reading Snapshot Data

Reading snapshot data can be done by overriding ReadSnapshot on a component. You can return a T ask

here to have the loading screen wait for this to be done before continuing.

void INetworkSnapshot.ReadSnapshot( ref ByteStream reader )

 var length = reader.Read<int>();
 MyVoxelData = reader.ReadArray<byte>( length ).ToArray();

 protected override Task OnLoad()
 await LoadVoxelWorld( MyVoxelData );

private Task LoadVoxelWorld( byte[] data )

Create d 17 Aug 2024

Updated 30 Jan 2025 about

Dedicated Servers

Installation

You can find information about how to install and use SteamCMD here

https://developer.valvesoftware.com/wiki/SteamCMD to install the s&box Dedicated Server.

Once SteamCMD has been installed, you can install or update the s&box Server by running the following

command from the directory you installed SteamCMD.

./steamcmd +login anonymous +app_update 1892930 validate +quit

You can use -beta staging to host a server on the staging branch, this might not be playable

by everyone though.

Running the Server

Once installed, the default directory would be steamcmd/steamapps/common/sbox dedicated server .

Windows

You can create a simple .bat file that will start your server. Here's an example, you could create a file

called Run-Server.bat that looks like this:

echo off
sbox-server.exe +game facepunch.sandbox facepunch.flatgrass +hostname My Dedicated Ser

Linux

The server runs on .NET , so you'll need the .NET Runtime installed. You can create a shell script to start your

server, for example run-server.sh :

#!/bin/bash
./sbox-server.exe +game facepunch.sandbox facepunch.flatgrass +hostname "My Dedicated

When run, this will load the facepunch.sandbox game with the facepunch.flatgrass map and the title

would be My Dedicated Server.

You can run the server with the following available command line parameters. These are just essentially a

ConVar or ConCmd that is run when the server boots up.

+game

You can pass a path to a .sbproj file to load a local project on a Dedicated Server. Connected

clients will receive code changes and hotload them.

S wit c h

A r g ume nt s

D e s c r ip t io n

<packageIdent>

The game package to load and optionally a map

[mapPackageIdent]

package.

+hostname

<name>

The server title that players will see.

+net_game_server_token

<token>

**This is not required and is only available as an option

once s&box is released.**Visit

https://steamcommunity.com/dev/managegameservers

to generate a token associated with your Steam Account.

You can use this token to ensure your Dedicated Server

always has the same Steam ID for other players to

connect to it. You don't need this, but otherwise every time

you load the server it will generate a new Steam ID.

+port

<port>

The port used to host the server on.

+net_query_port

<port>

The port used to query server information such as player

count, current map, etc.

Create d 7 Nov 2024

Updated 15 Apr 2025 about

Running Local Projects

When running a dedicated server - you have the option of running an entirely local project as the game.

I.e:

+game c:/git/sbox-mygame/.sbproj

Assets will still be fetched from the cloud version of the game - and stuff that is missing will be sent

directly from the server to clients, including code.

What about Serverside Code?

This is the only opportunity for running serverside code which can be safely hidden from clients. When

publishing a game, we'll strip out serverside code - this gives you the control, via your own servers.

Create d 9 Jul 2025

Updated 9 Jul 2025 about

Serverside Code

Serverside Code only works when running local projects - please read that page first.

What is it?

When compiling a project, if we're a dedicated server, we can run code in if #SERVER blocks.

protected override void OnUpdate()
#if SERVER
 Log.Info( $"This is a server update!" );
#else
 Log.Info( $"This is a client update!" );
#endif

If we're running on a dedicated server, we'll get This is a server update! spamming our console.

This is especially useful for omitting potentitally sensitive code from client builds, like contacting an API

server, or a database.

.Server.cs files

Say you have a GameManager.cs file, which has a partial class, you can accompany it with a

GameManager.Server.cs file which is safely omitted from client builds and wraps the whole file in an '#if

SERVER block - it's a nice bit of sugar that saves you having a bunch of preprocessor blocks in your code.

What if I publish my game?

All serverside code is stripped out of published games by default - so there's no worries there.

Updated 9 Jul 2025about gamesgames business_centerworkshop forumforum docsdocs Find Docs..
User Permissions
On a Dedicated Server, you can specify who is an admin of your server, or customize permissions even
further with claims for individual Steam accounts.
Users
On your Dedicated Server, you can edit the users/config.json file to add specific permissions per user.
The default config demonstrates how these are set up.
/* You can give a Steam account specific permissions here using their Steam Id. */
"SteamId": "00000000000000000",
"Claims": [ "kick", "ban", "restart" ],
"Name": "Example"
"SteamId": "00000000000000000",
"Claims": [ "kick", "ban", "restart" ],
"Name": "Example"
Claims
Claims are strings which describe actions that a user can take. You can add your own custom claims, as
they're just strings.
The host can check if a specific Connection has a permission with Connection.HasPermission( string ) .
By default, the host hasall permissions.
| | | |  🚀🪑💼🔩🧍🎎🎨🧑‍🤝‍🧑 GSCEEARN e t t i n g S t a r t e d | |
| --- | --- | --- | ---------------------------------------------------------- | --- |
P e rm i s si o n s ar e n o t netwo r c o e d n k e e e d right now, so only the host can check if a connection has a
|  | | | dx p i t o o rt r t i n g S t a n d a l o n e | |
| --------- | ----------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| | | | e s sn e dw e s r i nk g | |
| sp e ci f | ic p e r m i ss | io n . | 🔑albumsettings_input_hdmi CD C e u o t s n ti no o e m r c i t n S i gon a n & p P M s e h r u mor l t t i i s p D s l aia o t y na esr | |
| | | |  📂👾P e RS d ue nr c n a i n t e g d L oS e c ra v l e d P r s o j e c t s | |
| | | | lan📆🔌👁👾🛍✉🔄🥼  lock v U e s r s e i r d P e e C r m o i s e s i o n s | |
| | | | H NNNNORST t eeee t p tttt wwww R oooo e rrrr q kkkk u e EHV e v ei s e l t p n s te s ri | |
d s O i b b i l j et y c t s
Pyee w Cns n c eM n P r e s r o hs sp i p a e gr t e ip e s s
| | | | W b t S i o g c k M e u t ls t i l a y e r | |
| --- | --- | --- | -------------------------------------------- | --- |
| | | |  ⚡🖥🎮🍝🎬💿🔊🎮💽 PUGAMMSGS h I y s i c s | |
c a t m i o e n G M ra o a u p n h t s
oe d v i i e a M k e r 
| | | | o a u m n de p l a y | |
| --- | --- | --- | -------------------- | --- |
| | | | e r v i c e s | |

Created 17 Jan 2025
Updated 17 Jan 2025
News Docs Metrics FAQ Forum Discord Twitter
   🚀🪑💼🔩🧍🎎🎨🧑‍🤝‍🧑 ⚡🖥🎮🍝🎬💿🔊🎮💽 🔑albumsettings_input_hdmi lan📆🔌👁👾🛍✉🔄🥼 📂👾P GSCEEARN PUGAMMSGS  CD H W C NNNNORST dx c e h o e s I c e e o a a e t oe p RS u Pyee e i sn y r lock eeee t u o t w t t t d d m d m ue v v s o Cns e i p b n dw s tttt t o n o n i i ti n e nr i t wwww c i rt i e c c e a S e e de n r v c no o n R i t eM s n n U e a o r e p oooo P g i s M e G m e r M r n i i g s n s t e nk r s r c l c rrrr q g S s ra a e o e kkkk i g o hs g k t M n a S u i t d e r k y sp d i i e S u EHV gon p a L p e e d a u P v e t t e n oS ei a n s r h s r ls a & e e gr t t e l O t c t C p i t p r s P n b e n e i s ra ip m M s b e o e v te d d i s l l h l s e j s r ri d a a u i et P s mor y l e c y l r s s t t o o i t e i i s o p D n s j r s e n e l aia c o s t y t na s esr  about

Http Requests

s&box provides a static Http class, this lets you easily create asynchronous HT T P requests of different

methods (GET , POST , DELET E, etc…) providing JSON content and parsing JSON responses.

Allowed URLs

You can only use http or https URLs to domains (no IP addresses), and to prevent abuse, localhost is

permitted only on ports 80/443/8080/8443.

The command line switch -allowlocalhttp will let you access any local URL from the server.

Cheat Sheet

Some common things you might want to do…

// GET request that returns the response as a string
string response = await Http.RequestStringAsync( "https://google.com" );

// POST request of JSON content ignoring any response
await Http.RequestAsync( "https://api.facepunch.com/my/method", "POST", Http.CreateJso

Create d 26 Se p 2024

Updated 26 Se p 2024 about

Networking & Multiplayer

The networking system in s&box is purposefully simple and easy. Our initial aim isn't to provide a

bullet proof server-authoritative networking system. Our aim is to provide a system that is

really easy to use and understand.

Overview

Here's a quick cheat sheet for the network system, to get you started.

Creat e a new lobby

Networking.CreateLobby( new LobbyConfig()
 MaxPlayers = 8,
 Privacy = LobbyPrivacy.Public,
 Name = "My Lobby Name"

Listall available lobbies

list = await Networking.QueryLobbies();

Join an existing lobby

Networking.Connect( lobbyId );

Enable GameObject Networking

Destroy Networked GameObject

go.Destroy();

var go = PlayerPrefab.Clone( SpawnPoint.Transform.World );
go.NetworkSpawn();

RPCs

[Rpc.Broadcast]
public void OnJump()

Log.Info( $"{this} Has Jumped!" );

Create d 24 Nov 2023

Updated 15 Jun 2025 about

Networked Objects

Instantiating a Networked Object

Any game object can become a networked object by simply calling NetworkSpawn() on it. It will then be

sent toall clients and can have Sync Properties and RPC Messages.

Every networked game object can have an owner, which determines who sends updates about its position,

rotation and scale, as well as who can perform certain actions on it.

Network Mode

All game objects can be one of three network modes. This mode determines whether other clients see it,

or how they receive new information about it.

Mo d e

B e ha vio ur

NetworkMode.Never

This game object is never networked to others

NetworkMode.Object

The game object will be sent to other clients as its own networked object which

can have synchronized properties and RPCs

NetworkMode.Snapshot

The host will send this game object as part of the intitial scene snapshot when a

(default)

client joins the game

The network mode can also be changed for an object in the Scene from the Inspector view.

Interpolation

By default the transform ofall networked objects is interpolated smoothly for other clients.

Disabling Interpolation

// Disable interpolation for this networked object.
Network.DisableInterpolation();

Clearing Interpolation

Sometimes you want to clear any interpolation for an object. You can do that with

Network.ClearInterpolation() . If you are the owner of the object, other clients will be told to clear

interpolation when they next receive a transform update from us.

One use case for this would be to set the position of the object and have the position updated

immediately for everybody without interpolation (teleporting.)

Transform.Position = Vector3.Zero;
Network.ClearInterpolation();

Refreshing a Networked Object

Once you call NetworkSpawn() on a game object, any further changes to its components or

hierarchy will not be networked. Only information about the components or children that

existed when you network spawned it will be sent to other clients.

If you add new components, change the enabled state of a component, add new children or change the

hierarchy of a networked object significantly, you can send a refresh update to other clients by calling

Network.Refresh() on the networked game object or from one of its components.

By default, only the host can send refresh updates for networked objects. If you'd like to enable the owner

to also send refresh updates you can do so by changing the connection permissions for a client.

Create d 21 Mar 2024

Updated 30 Apr 2024 about

Network Events

Your games will likely want to react to people joining and leaving the game. To help with this you can

implement Component.INetworkListener or Component.INetworkSpawn on a component and place it in the

scene.

Example

Here's an example, where on joining the game a player object is created and the incoming player is

assigned as the owner.

public sealed class GameNetworkManager : Component, Component.INetworkListener

[Property] public GameObject PlayerPrefab { get; set; }
[Property] public GameObject SpawnPoint { get; set; }

/// <summary>
/// Called on the host when someone successfully joins the server (including the l
/// </summary>
public void OnActive( Connection connection )

// Spawn a player for this client
var player = PlayerPrefab.Clone( SpawnPoint.Transform.World );

// Find the NameTag component and set their name correctly
var nameTag = player.Components.Get<NameTagPanel>( FindMode.EverythingInSelfAn
if ( nameTag is not null )

nameTag.Name = connection.DisplayName;

// Spawn it on the network, assign connection as the owner
player.NetworkSpawn( connection );

INetworkListener

The interface INetworkListener has multiple methods that you can optionally override.

OnConnected

D e s c r ip t io n

The client has connected to the server. They're about to start handshaking, in which they'll

load the game and downloadall the required packages.

OnDisconnected

The client has disconnected from the server.

OnActive

The client is fully connected and completely the handshake. After this call they will close the

loading screen and start playing.

INetworkSpawn

The interface INetworkSpawn has a method to react to objects spawning on the network.

M e t h o d

D e s c r ipt io n

OnNetworkSpawn

Called when this object is spawned on the network.

Create d 25 Nov 2023

Updated 13 Mar 2024 about

Network Helper

To make a multiplayer game you need to take care of a few things. T here's a special component that

helps with those things, called NetworkHelper. This is a simple component that fits a lot of situations, but

can be used as an example to code your own network component.

Creating a server

If the StartServer property is enabled, a server will automatically be created when the scene is loaded.

That is unless the network system is already active (because you're joining a server using this scene).

Player Spawning

When a player enters a server you need to create an object for them to control. If it's a racing game, you'd

spawn them a car to control. If it's a shooter game, you'd spawn them a player.

Generally this is done using a prefab. You define your player gameobject and create a prefab, then you

can drag the prefab object into the PlayerPrefab property on the component.

You can also define a list spawnpoint GameObject's. The player will spawn randomly on one of them. If you

don't define any spawn points, they will spawn at the location of the NetworkHelper object.

Player Object

Your player object will usually contain a component with a function like this, which controls the

GameObject if it isn't a Proxy .

protected override void OnUpdate()

// If we're a proxy then don't do any controls
// because this client isn't controlling us!
if ( IsProxy )
return;

if ( !Input.AnalogMove.IsNearZeroLength )

WorldPosition += Input.AnalogMove.Normal * Time.Delta * 100.0f;

// position the camera
var camera = Scene.GetAllComponents<CameraComponent>().FirstOrDefault();
camera.WorldRotation = new Angles( 45, 0, 0 );
camera.WorldPosition = WorldPosition + camera.WorldRotation.Backward * 1500;

Under The Hood

NetworkHelper works by implementing Component.INetworkListener . This interface contains a method

that is called when a connection becomes active on the server.

In this method we create an instance of the PlayerPrefab and set the new client as its owner. The client

receives the information about this new object, and the fact that they're the owner, and takes over from

there.

Create d 14 De c 2023

Updated 3 O ct 2024 about

Network Visibility

Network Visibility & Culling

Network Visibility controls whether a networked object should be visible f or a specif ic player

(Connection). Visibility determines whether the object receives ongoing network updates — such as Sync

Vars and T ransform updates — for that client.

By default, all networked objects always transmit toall Connections, unless you explicitly disable this

behaviour.

Always T ransmit

Every networked object has flag called Always T ransmit.

Def ault: AlwaysTransmit = true

When true , the object never gets culled and is visible to every player.

This is the simple default for beginners, but for larger or more complex games, disabling Always T ransmit

can enable performance benefits by culling objects that the player should not receive updates for.

INetworkVisible Interf ace

You can take control of visibility by attaching a Component to the root GameObject of a networked

object that implements Component.INetworkVisible .

Only the owner of a networked object decides visibility for each connection.

public class MyVisibilityComponent : Component, INetworkVisible
 public bool IsVisibleToConnection( Connection connection, in BBox worldBounds )
 // Your visibility logic here…
 return true;

IsVisibleToConnection Paramet ers

D e s c r ip t io n

Connection connection

The target player being tested.

BBox worldBounds

The object's world-space bounding box. Helpful for distance or frustum checks.

Return true if the object should be visible to that connection; f alse if it should be culled.

To enable this behaviour, disable AlwaysTransmit on the root network object.

Hammer PVS Integration

If no component implementing INetworkVisible exists on the root GameObject and the map is a

Hammer map with VIS compiled:

The engine automatically falls back to PVS (Potentially Visible Set).

Visibility is determined using Hammer's visibility data.

This is an ideal default for static world objects on Hammer maps.

What Happens When an Object Is Culled?

When the owner decides an object is not visible to a connection:

The following stop being sent:

Sync Var updates

T ransform updates

The following still occur:

The object still spawns for the client.

The object becomes Disabled locally for that client while hidden.

RPCs are still delivered.

Invisible objects remain known to the client, just not updated.

Create d 14 Nov 2025

Updated 19 Nov 2025 about

Ownership

Networked GameObjects can be owned by a connection.

Objects that are owned by a connection are simulated by that connection. T heir position and their

variables areall controlled by the controlling client.

If an object is unowned by a connection then it is simulated by the host.

Owner T ransf er

By default, a networked object's owner can only be changed by the host. However, the current owner of

the object can change that behavior by setting its OwnerTransfer value.

// Make it so anyone can change the owner of this networked object.
go.Network.SetOwnerTransfer( OwnerTransfer.Takeover );

T yp e

B e ha vio ur

OwnerTransfer.Takeover

Anyone can change the owner

OwnerTransfer.Fixed (default)

Only the host can change the owner

OwnerTransfer.Request

A request must be made to the host to change the owner

Getting the Owner

You can find the owner of a GameObject by checking Network.OwnerId .

public override void Update()

Log.Info( $"Owner is {Network.OwnerId}" );

In reality, day to day, you won't really be interested in the particular owner. You only care about whether

you're meant to be simulating it or not. You do that by checking IsProxy - which is true if the

GameObject is being simulated by another client (or the server).

public override void Update()

 if ( IsProxy ) return;

 // if we pressed E, try to pick something up
 if ( Input.Pressed( "use" ) )
 TryPickup();

T aking Ownership

You can take ownership of an object, which makes you the simulator.

void TryPickup()

// are we looking at anything?
var tr = Physics.Trace.WithoutTags( "player" )

.Sphere( 16, EyePos, EyePos + LookDir.Forward * 100 )
.Run();

if ( !tr.Hit ) return;

if ( tr.Body.GameObject is not GameObject go )

return;

if ( !go.Tags.Has( "pickup" ) )

return;

 // You're my wife now

go.Network.TakeOwnership();

 // Store that we're carrying it

Carrying = go;

So for example, if a player picks up an object, the player could take ownership of that object. That way the

position is controlled by that player.

If a player gets in a car, you could make the player the owner of that car - then its position will be

controlled by that player.

And of course, the player is generally controlled by its own connection.

Dropping Ownership

You can also stop owning an object. At that point the object becomes owned by the server.

void ThrowObject()

if ( !Carrying.IsValid() )

return;

// Stop owning this

Carrying.Network.DropOwnership();
Carrying = null;

Default Owners

If you make an object in the scene editor networked, by default it will not have an owner. It will be

simulated by the host.

When a client creates a network object via GameObject.NetworkSpawn() , they will be the owner of that

object.

Disconnection

By defaultall networked objects that a client owns will be destroyed for everyone when they disconnect.

You can change this by setting the Orphaned Mode for that networked object. Only the current owner

can change the Orphaned Mode.

Simply call GameObject.Network.SetOrphanedMode with one of the following options:

T yp e

B e ha vio ur

NetworkOrphaned.Destroy

(default)

The object will be destroyed when the owner disconnects

NetworkOrphaned.Host

The host will be assigned ownership when the current owner disconnects

NetworkOrphaned.Random

A random client will be assigned ownership when the current owner

disconnects

NetworkOrphaned.ClearOwner

The object will remain but ownership will be cleared (the host will

simulate the object)

Create d 24 Nov 2023

Updated 28 Mar 2024 about

RPC Messages

Components can contain RPCs. An RPC is a function that when called, is called remotely too.

Supported RPC arguments are the exact same as Sync properties.

Example

Imagine your game has a button, and you want it to make a bing noise when it's pressed. You could have a

function like this.

void OnPressed()

Sound.Play( "bing", WorldPosition );

The problem here is, that sound is only played on the host, or on the client where OnPressed is called. You

want everyone to hear that sound. So you instead do something like this.

void OnPressed()

PlayOpenEffects();

[Rpc.Broadcast]
public void PlayOpenEffects()

Sound.Play( "bing", WorldPosition );

The attribute [Rpc.Broadcast] makes it so when you call that function, it broadcasts a network message

to everyone to call that function too. Without any flags, anyone could technically call that function, but

you could add flags to restrict it to only the host, or only the owner of the object. See the Flags section

below for more details.

Static RPC

Static methods can be RPCs, too. A static RPC does not need to exist on a Component but can exist as a

method on any static class.

public static void PlaySoundAllClients( string soundName, Vector3 position )

Sound.Play( soundName, position );

Rpc.Owner

Unlike [Rpc.Broadcast] which calls the function for everybody, you can use [Rpc.Owner] instead which

means that the function will only be called for the Owner of the networked object or the host if the object

has no owner.

Rpc.Host

Similarly to Rpc.Owner, adding this will mean the function is only called on the Host.

Flags

When defining an RPC, you can define a number of flags.

[Rpc.Broadcast( NetFlags.Unreliable | NetFlag.OwnerOnly )]
public static void PlaySoundAllClients( string soundName, Vector3 position )

Na me

D e s c r ip t io n

NetFlags.Unreliable

NetFlags.Reliable

Message will be sent unreliably. It may not arrive and it may be received out of

order. But chances are that it will arrive on time and everything will be fine. This is

good for sending position updates, or spawning effects. This is the fastest way to

send a message. It is also the cheapest.

This is the default, so you don't need to specify this. Message will be sent reliably.

Multiple attempts will be made until the recipient has received it. Use this for things

like chat messages, or important events. This is the slowest way to send a

message. It is also the most expensive.

NetFlags.SendImmediate

Message will not be grouped up with other messages, and will be sent

immediately. This is most useful for things like streaming voice data, where

packets need to stream in real-time, rather than arriving with a bunch of other

packets.

NetFlags.DiscardOnDelay

Message will be dropped if it can't be sent quickly. Only applicable to unreliable

messages.

NetFlags.HostOnly

This RPC can only be called from the Host.

NetFlags.OwnerOnly

This RPC can only be called from the owner of the object it's being called on. 

You can pass arguments to the RPC like any other method, and they'll get passed magically.

void OnPressed()

PlayOpenEffects( "bing", WorldPosition );

[Rpc.Broadcast]
public void PlayOpenEffects( string soundName, Vector3 position )

Sound.Play( soundName, position );

Filtering

You can filter the recipients of a Broadcast RPC. This allows you to exclude specific connections from

receiving the RPC, or only include specific connections.

// Don't send the RPC to player's called Harry (sorry Harry!)
using ( Rpc.FilterExclude( c => c.DisplayName == "Harry" ) )

PlayOpenEffects( "bing", WorldPosition );

// Only send the RPC to player's called Garry.
using ( Rpc.FilterInclude( c => c.DisplayName == "Garry" ) )

PlayOpenEffects( "bing", WorldPosition );

Caller Information

You can check which connection called the method using the Rpc.Caller class.

void OnPressed()

PlayOpenEffects( "bing", WorldPosition );

[Rpc.Broadcast]
public void PlayOpenEffects( string soundName, Vector3 position )

if ( !Rpc.Caller.IsHost ) return;

Log.Info( $"{Rpc.Caller.DisplayName} with the steamid {Rpc.Caller.SteamId} played
Sound.Play( soundName, position );

Updated 29 Nov 2024 about

Sync Properties

Sync Attribute

Adding the [Sync] attribute to a property on a Component will have its latest value sent to other players

each time it changes.

public class MyComponent : Component
 [Sync] public int Kills { get; set; }

These properties are controlled by the owner of the object, therefore only the owner of the object can

change them.

Supported Types

[Sync] properties support unmanaged types, and string. You can't synchronize every class with them, but

any value type including structs will be fine. int , bool , Vector3 , float areall examples of valid types.

We also support serializing specific classes such as GameObject , Component , GameResource .

Detecting Changes

You can detect changes to a [Sync] property by also applying a the [Change] attribute to it. With this

attribute you can specify the name of a callback method that will be invoked when the value of the

property has changed.

Right now the [Change] attribute will not invoke the callback when a collection has changed.

The callback will only be invoked when the property itself is assigned to something different.

public class MyComponent : Component
 [Sync, Change( "OnIsRunningChanged" )] public bool IsRunning { get; set; }

 private void OnIsRunningChanged( bool oldValue, bool newValue )
 // The value of IsRunning has changed...

Sync Flags

You can customize the behaviour of a synchronized property with SyncFlags .

F la g

D e s c r ipt io n

SyncFlags.Query

Enables Query Mode for the property. See the Query Mode section below.

SyncFlags.FromHost

The host has ownership over the value, instead of the owner of the networked

object. Only the host may change the value.

SyncFlags.Interpolate

The value of the property will be interpolated for other clients. The value is

interpolated over a few ticks.

Collections

Sometimes you want to network collections such as an entire list or a dictionary. We provide special

classes to do that.

public enum AmmoCount
 Pistol,
 Rifle

public class MyComponent : Component
 [Sync] public NetList<int> List { get; set; } = new();
 [Sync] public NetDictionary<AmmoCount,int> Dictionary { get; set; } = new();

You can initialize each in the declaration with new() or you can initialize the lists elsewhere, so long as

you're doing so on the Owner of the network object. It doesn't matter if they are null for anyone else

because they'll get created when they are networked if they need to be.

You can use NetList<T> and NetDictionary<K,V> like their regular counterparts. They contain indexers,

Add , Remove and other methods you'd expect.

NetList and NetDictionary do not currently support the [Property] attribute.

Query Mode

By default the properties are automatically marked dirty when set, via codegen magic.. meaning that

when you set a property, if it's different we'll send the updated value to everyone.

public Vector3 Velocity

get;
set;

No Query Mode needed. The only way to change Velocity is via the setter, which when called will mark it as

changed using invisible codegen magic on the setter.

Vector3 _velocity;
[Sync]
public Vector3 Velocity

get => _velocity;
set => _velocity = value;

Again - no Query Mode needed. The only way we're setting _velocity is via the setter - so it can never get

out of date.

Vector3 _velocity;
[Sync( SyncFlags.Query )]
public Vector3 Velocity

get => _velocity;
set => _velocity = value;

void SetVelocity( Vector3 val)
 _velocity = val;

Query Mode needed - because when you call SetVelocity it changes _velocity and the network system

doesn't know that the Velocity value has changed. This could be avoided in that case by setting

Velocity instead of _velocity .

With SyncFlags.Query , the variable is instead checked for changes every network update, and sent if

changed. This is marginally slower than non-query mode, but it means that you can sync special stuff like

this.

Create d 10 Jan 2024

Updated 30 Jan 2025 about

Testing Multiplayer

The number one best way to test multiplayer is to have someone join your game.. but that's obviously not

always possible.

New Instance

For this reason you can spawn another instance of the game, which will join your currently running session.

To do this, click on the network status icon in the header bar, and select Join via new instance.

A new instance of the game will appear and join your game.

Iterating

You can continue to code on your main instance, with the game running and the other instance joined.

The code changes will be mirrored to the other client. In fact, they'll be mirrored toall clients - so even if

you have a friend join, their game will update.

Reconnect

If you need to reconnect, you can do this via the reconnect command.

Joining manually

You can open an instance and manually join your local editor session by running connect local in the

console.

Updated 28 Mar 2024 about

WebSockets

s&box allows you to use WebSockets to interface with an external server. Common usages include custom

networking, or persistent data outside of a local filesystem.

Connection and Messaging

Adding this Component to a GameObject in the Scene will ensure the connection is started when the

game starts.

public sealed class Server : Component

// Example: wss://host.example:443/ws
[Property] public string ConnectionUri { get; set; }
public WebSocket Socket { get; set; }

protected override void OnStart()

Socket = new WebSocket();
Socket.OnMessageReceived += HandleMessageReceived;
_ = Connect();

// Connect to the server and send a message
private async Task Connect()

await Socket.Connect( ConnectionUri );
await SendMessage( "Hello!" );

private async Task SendMessage( string message )

await Socket.Send( message );

// Log our received messages
private void HandleMessageReceived( string message )

Log.Info( message );

You could attach an Auth T oken to your WebSocket request header like so:

var token = await Sandbox.Services.Auth.GetToken( "YourServiceName" );

if ( string.IsNullOrEmpty( token ) )

// Unable to fetch a valid session token
return;

var headers = new Dictionary<string, string>()

{ "Authorization", token }

await socket.Connect( "ws://localhost:8080", headers );

Create d 26 Se p 2024

Updated 26 Se p 2024 about

Physics

S&box includes a full 3D and 2D physics system powered by the Source 2 engine, with great performance

and stability. Rigidbodies, colliders, joints, raycasting, and trigger volumes areall usable through

Components on GameObjects.

In This Section

🎯 T racing — Raycasting and shape traces (ray, sphere, box) with collision rules and tag filtering
🚪 T riggers — Detect when objects enter or exit a volume, without blocking movement
🚪 Physics Events — Hook into the physics step with PrePhysicsStep and PostPhysicsStep

Related

Player Controller — Physics-based character controller component

T errain Materials — Physics surface properties for terrain

Create d 10 Apr 2026

Updated 11 Apr 2026 about

IScenePhysicsEvents

This interface allows you to wrap logic around the physics step. This can be useful when you have an

object, or a system, that works closely with the physics system.

public interface IScenePhysicsEvents : ISceneEvent<IScenePhysicsEvents>

/// <summary>
/// Called before the physics step is run. This is called pretty much
/// right after FixedUpdate.
/// </summary>
void PrePhysicsStep() { }

/// <summary>
/// Called after the physics step is run
/// </summary>
void PostPhysicsStep() { }

Create d 30 O ct 2024

Updated 30 O ct 2024 about

Tracing

Scenes can be traced against using Scene.Trace - which uses a builder pattern to make construction a

bit easier. At a minimum, traces have a shape, start, and end. You can also filter which specific tags will be

hit or ignored, or opt-in to using your project's collision rule matrix by calling WithCollisionRules(tag) .

Here are some examples.

Simplest Trace

SceneTraceResult tr = Scene.Trace.Ray( startPos, endPos ).Run();

if ( tr.Hit )

Log.Info( $"Hit: {tr.GameObject} at {tr.EndPosition}" );

Use Collision Rules

This will fire a ray using the collision rules of a bullet tag, as configured in your project's Collision settings.

var tr = Scene.Trace

.Ray( startPos, endPos )
.WithCollisionRules( "bullet" ) // Hits everything that a bullet would hit
.Run();

Sphere Trace

var tr = Scene.Trace

.Sphere( 32.0f, startPos, endPos ) // 32 is the radius
.WithoutTags( "player" ) // ignore GameObjects with this tag
.Run();

Box Trace

var tr = Scene.Trace

.Ray( start, end )

.Size( new BBox( -5, 5 ) ) // size of the aabb
.UseHitboxes( true ) // hit hitboxes too!
.Run();

Debugging traces

You can visualize traces in the editor by calling DebugOverlay.Trace(tr) - this will draw the trace and the

hit point if there was a hit.

var tr = Scene.Trace
 .Ray( start, end )
 .Run();

DebugOverlay.Trace( tr, 5f ); // lasts for 5 seconds

Create d 28 De c 2023

Updated 15 May 2024 about

Triggers

A trigger is a collider that detects when other physics objects enter or exit it, without blocking their

movement. They're useful for things like pickup zones, death planes, checkpoints, and area detection.

Setting Up a Trigger

Any collider can become a trigger. In the inspector, tick the Is T rigger checkbox on a BoxCollider ,

SphereCollider , CapsuleCollider , or any other collider component.

To do it in code:

var box = AddComponent<BoxCollider>();
box.Scale = new Vector3( 200, 200, 100 );
box.IsTrigger = true;

Reacting to Trigger Events

Add Component.ITriggerListener to any component on the same GameObject as the trigger collider (or

a child). Implement OnTriggerEnter and OnTriggerExit :

public sealed class PickupZone : Component, Component.ITriggerListener

public void OnTriggerEnter( Collider other )

Log.Info( $"{other.GameObject.Name} entered the pickup zone" );

public void OnTriggerExit( Collider other )

Log.Info( $"{other.GameObject.Name} left the pickup zone" );

You can also use the overloads that give you both colliders if you need to know which trigger was hit

(useful when one GameObject has multiple triggers):

public void OnTriggerEnter( Collider self, Collider other )

And there are GameObject variants if you only care about the entering object, not its specific collider:

public void OnTriggerEnter( GameObject other ) { }
public void OnTriggerExit( GameObject other ) { }

The default player controller setup uses two child colliders for the player: a capsule for the body

and a box for the feet. When entering a trigger, you might get two events (one for each

collider), and neither of them will be the actual player GameObject. Use FindMode.InAncestors

to check for the player component in the parent GameObject.

Checking What's Inside (Polling)

If you'd rather poll than use events, Collider.Touching gives youall colliders currently overlapping this

trigger:

[Property] public BoxCollider Box { get; set; }

protected override void OnUpdate()
 foreach ( var collider in Box.Touching )
 Log.Info( $"{collider.GameObject.Name} is inside the box" );

The trigger fires OnTriggerExit automatically when a collider inside the trigger is disabled or

destroyed, so you don't need to manually clean up the list for disabled objects.

Create d 3 May 2026

Updated 3 May 2026 about

Rendering

Rendering, shaders, visual effects, and post-processing in s&box.

Ef f ects

Particle effects, beams, decals, and indirect lighting.

Post Processing

Screen-space effects like tonemapping, film grain, and custom post-processing.

Shader Graph

Visual node-based shader editor for creating custom materials.

Shaders

Writing shaders in code — HLSL shading models, render states, and GPU instancing.

Create d 10 Apr 2026

Updated 10 Apr 2026 about

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

Updated 10 Apr 2026about gamesgames business_centerworkshop forumforum docsdocs Find Docs.. about

Auth Tokens

If you are using HT T P requests or WebSockets in your game, you can use Auth T okens to validate that the

requests were sent from a valid Steam user in a s&box game session. This is useful if you want to tie data

to a specific Steam account, or prevent botting.

Generating Tokens

You can generate a new token with Sandbox.Services like so:

var token = await Sandbox.Services.Auth.GetToken( "YourServiceName" );

Validating Tokens

To validate a token on your backend, you need to make a call to the services.facepunch.com/sbox API

using the auth/token endpoint.

Here is an example of how to validate a token in C# using System.Net.Http

private class ValidateAuthTokenResponse

public long SteamId { get; set; }
public string Status { get; set; }

public static async Task<bool> ValidateToken( long steamId, string token )

var http = new System.Net.Http.HttpClient();
var data = new Dictionary<string, object>

{ "steamid", steamId },
{ "token", token }

var content = new StringContent( JsonSerializer.Serialize( data ), Encoding.UTF8,
var result = await http.PostAsync( "https://services.facepunch.com/sbox/auth/token

if ( result.StatusCode != HttpStatusCode.OK ) return false;

var response = await result.Content.ReadFromJsonAsync<ValidateAuthTokenResponse>()
if ( response is null || response.Status != "ok" ) return false;

At some point when receiving the token from the client on your backend you can then validate it as such:

var isValidToken = await ValidateToken( steamId, token );

if ( isValidToken )

Console.WriteLine( "Success!" );

Create d 22 De c 2023

Updated 14 Aug 2025 about

Leaderboards

Leaderboards are just stats, aggregated and ordered.

Basic Example

Here's how to get a leaderboard. We want to get a leaderboard to show who has killed the most zombies,

globally.

var board = Sandbox.Services.Leaderboards.GetFromStat( "facepunch.ss1", "zombies_kille
await board.Refresh();

foreach ( var entry in board.Entries )

Log.Info( $"{entry.Rank} - {entry.DisplayName} - {entry.Value}" );

By default, leaderboards are aggregated using the sum ofall the stats and ordered descending.

By Country

You can filter a leaderboard by country. This will only show stats that were created in that country.

var board = Sandbox.Services.Leaderboards.GetFromStat( "facepunch.ss1", "zombies_kille
board.SetCountryCode( "gb" );
await board.Refresh();

foreach ( var entry in board.Entries )

Log.Info( $"{entry.Rank} - {entry.DisplayName} - {entry.Value} [{entry.CountryCode

By Date

If you pass countrycode as "auto" it will use the current player's location

You can filter leaderboards by date, allowing yearly, weekly, monthly or daily leaderboards.

board.FilterByMonth();
board.SetDatePeriod( new System.DateTime( 2024, 8, 1 ) );
await board.Refresh();

foreach ( var entry in board.Entries )

Log.Info( $"{entry.Rank} - {entry.DisplayName} - {entry.Value} [{entry.CountryCode

If you don't set a date period, it'll use the current date

Centering

You can focus the leaderboard on a certain player. This will show the results around that player. It is nice to

show a player's contemperies rather than showing the top 20all the time.

var board = Sandbox.Services.Leaderboards.GetFromStat( "facepunch.ss1", "zombies_kille
board.CenterOnSteamId( 76561197960279927 );
await board.Refresh();

foreach ( var entry in board.Entries )

Log.Info( $"{entry.Rank} - {entry.DisplayName} - {entry.Value}" );

You can also call .CenterOnMe() to center on the local player.

Aggregation and Sorting

So maybe instead of the sum of something, we want to show people's shortest result. Like in this example,

we're showing a list of the fastest win times.

var board = Sandbox.Services.Leaderboards.GetFromStat( "facepunch.ss1", "victory_elaps

board.SetAggregationMin(); // select the lowest value from each player
board.SetSortAscending(); // order by the lowest value first
board.FilterByMonth(); // only show results from this month
board.CenterOnMe(); // offset so I'm in the middle of the results
board.MaxEntries = 100;

await board.Refresh();

foreach ( var entry in board.Entries )

Log.Info( $"{entry.Rank} - {entry.DisplayName} - {entry.Value} [{entry.Timestamp}]

The entry timestamp holds the time of the selected result

Create d 23 Aug 2024

Updated 23 Aug 2024 about

Web Api

The API for leaderboards is publically accessible. Have fun!

https://services.facepunch.com/sbox/package/leaderboard/{package_ident}/

st at

The name of the stat to base the leaderboard on. This does not need to have been registered formally.

count (default 10)

The amount of results to return

offset (default 0)

If higher than 0 then the results will start at this number. If lower than 0, we'll start at the bottom of the

results. For example, a value us -1 will return the very last page of results.

aggregation (default sum)

Describes how to aggregate the stats. This is fundamental to getting the leaderboard in a format that

makes sense.

sum

max

min

avg

A d d s a ll va lue s t o g e t he r . This is us e f ul f o r t hing s like t he mo s t kills , whe r e yo u

ha ve a s t a t t ha t is inc r e me nt e d o n e a c h kill.

The maximum single value every submitted. An example would be for high scores.

The lowest value every submitted. You could use this for fastest time etc.

The average value from every value submitted. I can't think of a use case.

last

The last value submitted. I can't think of a use case.

sort (default desc)

How the leaderboard values should be sorted.

desc

H ig he s t va lue s f ir s t

asc

Lowest values first

Allows querying a specific time period for a leaderboard. This allows creating things like weekly

leaderboards.

none

D o no t limit b y t ime p e r io d .

year

month

week

day

Limit by year

Limit by month

Limit by week

Limit by day

dat e (default now)

Allows specifying a date to get for datefilter. You don't need to be exact with the date, it just has to be

within the period you want to get. If unset, will default to now - which will get the current leaderboard for

any datefilter.

This does nothing if datefilter is none.

cent erst eamid (default 0)

Center the results on a certain SteamId within the board. Offset will offset from this position.

count ry (default none)

Limit results to a specific country code. If set to auto this will return the current user's country, if logged in.

friends (default false)

Limit results to the current logged user's friends.

include[] (default null)

Allows a list of steamids to always show on the leaderboard, even if they're not in current subset. This is

useful for situations where you want to show the top 20, but want the current player's score to be present

too.

Example

https://services.facepunch.com/sbox/package/leaderboard/facepunch.ss1/?stat=zombies_ki

 Stat: "zombies_killed",
 TotalEntries: 2588,
 Entries:
 Rank: 1,
 Value: 645806,

 CountryCode: "us",
 DisplayName: "puxorb",
 Timestamp: "2024-08-23T03:44:17.0174014+00:00",
 Data: { }
 Rank: 2,
 Value: 310250,
 SteamId: 76561198053736750,
 CountryCode: "au",
 DisplayName: "Rin",
 Timestamp: "2024-08-19T18:28:10.6930596+00:00",
 Data: { }
 DateDescription: null,

Create d 23 Aug 2024

Updated 23 Aug 2024 about

Services

Backend services for achievements, leaderboards, stats, and authentication.

Achievements

T rack and award player achievements.

Leaderboards

Ranked leaderboard system with web API access.

Stats

Player statistics tracking.

Auth T okens

Authentication tokens for backend service calls.

Create d 23 Aug 2024

Updated 10 Apr 2026 about

Stats

Your game can record stats for each player that plays it. Here are some examples of things stats can

record.

Number of zombies killed

Fastest time

T otal meters walker

Coins collected

Longest time

Bullets fired

Kills per weapon

You can query and display these stats, or use them in any other way you want. You can query stats from

individual players, and you can get the compound stats globally.

Recording Stats

Depending on what you're doing, you either want to increment your stat..

public void OnZombieKilled()
    Sandbox.Services.Stats.Increment( "zombies-killed", 1 );

Or just set it directly..

public void OnGameFinished()
    Sandbox.Services.Stats.Increment( "wins", 1 );
    Sandbox.Services.Stats.SetValue( "win-time", SecondsTaken );

You can call these apis as often as you like. We batch the stats and send them when we're

ready.

You can also add data when calling SetValue. This is in the format of a Dictionary<string, object> and

this data is available when querying leaderboards.

Stats are available in two forms. Either global, or player.

// get global zombie kill count
var zombies = Sandbox.Services.Stats.Global.Get( "zombies_killed" );

Log.Info( $"there have been {zombies.Sum} zombies killed by {zombies.Players} players!

// Get local player zombie kill count
var zombies = Sandbox.Services.Stats.LocalPlayer.Get( "zombies_killed" );

Log.Info( $"You have killed {zombies.Sum} zombies!" );

// Get stats for Garry in SS1
var stats = Sandbox.Services.Stats.GetPlayerStats( "facepunch.ss1", 76561197960279927

// wait for them to download
await stats.Refresh();

var zombies = stats.Get( "zombies_killed" );

Log.Info( $"Garry has killed {zombies.Sum} zombies!" );

Create d 23 Aug 2024

Updated 9 Se p 2024 about

Sound

s&box has a full audio system including 2D/3D sound playback, voice chat, positional audio, an audio

effects pipeline, and lip sync support.

For music and programmatic audio streaming, see Audio.

Components

Audio components can be added to any GameObject in the editor. They handle everything from positional

sounds and soundscapes to voice chat and lip sync.

Co mp o ne nt

D e s c r ip t io n

SoundPointComponent

Plays a sound at a point in the world

SoundBoxComponent

Plays a sound within a box area

SoundscapeTrigger

Plays a soundscape when the listener enters the trigger area

AudioListener

Overrides where the client hears audio from, instead of the camera

LipSyncComponent

Drives morphs with lipsync from sounds

VoiceComponent

Records and transmits microphone input to other players

In This Section

Playing Sounds — Sound.Play , SoundHandle , GameObject.PlaySound , and audio components

Create d 22 Apr 2026

Updated 22 Apr 2026 about

Playing Sounds

s&box provides several ways to play sounds in code. You can fire-and-forget a sound at a world position,

control it via a SoundHandle , attach it to a GameObject , or use scene components entirely.

SoundEvent

Most sounds in s&box are defined as SoundEvent assets ( .sound files). A SoundEvent bundles one or

more audio files together with settings like volume range, pitch range, 3D distance, occlusion, and a

selection mode (random, sequential, etc.).

Reference a SoundEvent from a property on your component:

[Property] public SoundEvent FootstepSound { get; set; }

You can also load one by path at runtime:

var sound = ResourceLibrary.Get<SoundEvent>( "sounds/footsteps/concrete.sound" );

The UI flag on a SoundEvent makes it play as a flat 2D sound with no distance attenuation -

useful for interface and HUD audio.

Sound.Play

Sound.Play is the primary static API for playing sounds in code. It returns a SoundHandle you can use to

control the sound later.

Basic playback

// By SoundEvent reference
Sound.Play( FootstepSound );

// By asset path (string)
Sound.Play( "sounds/explosion.sound" );

// By asset name (string), can be placed in any folder but must be unique
Sound.Play( "explosion_large" );

3D posit ional sound

Pass a world-space Vector3 to place the sound in the scene:

Sound.Play( ExplosionSound, WorldPosition );
Sound.Play( "sounds/explosion.sound", transform.Position );

Without a position the sound defaults to the world origin (0, 0, 0) . For a sound that should follow an

object, use GameObject.PlaySound instead (see below).

Fade in

An optional fadeInTime parameter fades the volume up from silence over the given number of seconds:

Sound.Play( AmbientSound, WorldPosition, fadeInTime: 2.0f );

SoundHandle

Every Sound.Play call returns a SoundHandle . Keep a reference to it when you need to change or stop the

sound after it starts.

SoundHandle _engineLoop;

void StartEngine()
 _engineLoop = Sound.Play( EngineLoopSound, WorldPosition );
 _engineLoop.Volume = 0.8f;
 _engineLoop.Pitch = 1.2f;

Key propert ies

P r o p e r t y

D e s c r ip t io n

Position

World-space position of the sound

Volume

Pitch

Volume multiplier (default 1.0 )

Pitch multiplier (default 1.0 , 2.0 = one octave up)

Distance

Max audible distance in units (default 15 000)

SpacialBlend

0 = fully 2D, 1 = fully 3D (default 1.0 )

Occlusion

IsPlaying

Paused

Time

Whether geometry can block the sound (default true )

true while the sound is still active

Pause or resume without stopping

Playback position in seconds (seekable)

D e s c r ip t io n

TargetMixer

Route to a specific audio mixer

St opping a sound

// Instant stop
_engineLoop.Stop();

// Fade out over 1.5 seconds
_engineLoop.Stop( 1.5f );

After Stop() the handle becomes invalid. Accessing properties on an invalid handle is safe - they simply

do nothing.

St op everyt hing

Sound.StopAll( fade: 0.5f );

GameObject.PlaySound

GameObject.PlaySound plays a sound that f ollows the GameObject's world position every frame. This is

the recommended way to play sounds on moving objects - footsteps, projectile impacts, character voices.

// Plays the sound at this object's position and follows it
var handle = GameObject.PlaySound( FootstepSound );

// Plays the sound at around the player's head - offset is local
var handle = GameObject.PlaySound( FootstepSound, Vector3.Up * 64f );

The returned SoundHandle is just like any other - you can adjust volume, pitch, or call Stop() on it.

St oppingall sounds on a GameObject

// Stops every sound currently following this GameObject
GameObject.StopAllSounds();

// Fade out over 0.5 seconds
GameObject.StopAllSounds( fadeOutTime: 0.5f );

GameObject.PlaySound internally sets SoundHandle.Parent and SoundHandle.FollowParent =

true . You can do this manually for sounds started with Sound.Play if you need the same

behaviour:

var handle = Sound.Play( FootstepSound, WorldPosition );
handle.Parent = GameObject;
handle.FollowParent = true;

For sounds that don't need runtime code control, add one of these components to a GameObject in the

editor:

Co mp o ne nt

D e s c r ip t io n

SoundPointComponent

Plays a sound at a fixed world point. Supports auto-play, looping, and a randomised

repeat interval.

SoundBoxComponent

Like SoundPointComponent , but the source position is constrained to a box region.

SoundscapeTrigger

Blends in an ambient soundscape when the audio listener enters the trigger.

AudioListener

Overrides the listening position. Without this, audio is heard from the camera.

AudioList ener

By default the player hears sounds from the camera's position. Add an AudioListener component to a

different GameObject (e.g., the player's head bone) to move the listening point.

Create d 4 May 2026

Updated 4 May 2026 about

HudPainter

Each camera has a HudPainter that can be used to draw onto the HUD. You do this every frame, in any

Update function.

This is more efficient than using actual UI panels because there's no layout, stylesheets or interactivity..

you're doingall that stuff yourself.

If your UI is relatively simple, you can do it this way to keep things easy.

protected override void OnUpdate()

if ( Scene.Camera is null )

return;

var hud = Scene.Camera.Hud;

hud.DrawRect( new Rect( 300, 300, 10, 10 ), Color.White );

hud.DrawLine( new Vector2( 100, 100 ), new Vector2( 200, 200 ), 10, Color.Whit

hud.DrawText( new TextRendering.Scope( "Hello!", Color.Red, 32 ), Screen.Width

Create d 7 Nov 2024

Updated 28 Jun 2025 about

Localization

When displaying text such as Hello World , you should instead use a localization token like

#menu.helloworld . This will automatically replace the text with the corresponding language set by the user

when set on a Label, allowing you to easily support multiple languages.

Tokens

In UI, any displayed string that begins with a # will be recognized as a token, which means it will look for it's

real value in the localization system.

Example

Filename: Localization/en/sandbox.json

 "menu.helloworld": "Hello World",
 "spawnmenu.props": "Models",
 "spawnmenu.tools": "Tools"
 "spawnmenu.cloud": "sbox.game",

T hen it's as easy as doing the following:

<label>#spawnmenu.props</label>

Languages

Eng lis h Na me

A P I L a ng ua g e Co d e

Arabic

Bulgarian

Simplified Chinese

Traditional Chinese

Czech

ar

bg

zh-cn

zh-tw

cs

A P I L a ng ua g e Co d e

Danish

Dutch

English

Finnish

French

German

Greek

Hungarian

Italian

Japanese

Korean

Norwegian

Pirate

Polish

Portuguese

Portuguese-Brazil

Romanian

Russian

Spanish-Spain

Spanish-Latin America

Swedish

Thai

Turkish

Ukrainian

Vietnamese

da

nl

en

fi

fr

de

el

hu

it

ja

ko

no

en-pt

pl

pt

pt-br

ro

ru

es

es-419

sv

th

tr

uk

vn

Create d 24 Se p 2024

Updated 24 Se p 2024 about

UI

Our UI system is structured around Panels. A Panel is a c# class that can have parent and child panels.

The panels use a stylesheet and flex system for layout and rendering.

They can be created directly in code or via Razor files with HT ML/CSS syntax.

Making a C# Panel

Here's a basic example of a Panel that simply displays Time.Now :

public class MyPanel : Panel
 public Label MyLabel { get; set; }

 public MyPanel()
 MyLabel = new Label();
 MyLabel.Parent = this;

 public override void Tick()
 MyLabel.Text = $"{Time.Now}";

Using a Panel

Once you've create a Panel, it can be used in two different ways. The first is done identically to how we

added a Label in the example above:

var myPanel = new MyPanel();
myPanel.Parent = this;

The other is by using the following syntax within a [Razor Panels] file:

<MyPanel />

Creating a C# Root Panel

To draw your UI to either the Screen or to a World Panel, you'll need to create a PanelComponent. A

PanelComponent acts as the root ofall UI, and is added to any GameObject with either a ScreenPanel or

WorldPanel component. Here's an example of how you can create a basic one including the above panel:

public sealed class MyRootPanel : PanelComponent

MyPanel myPanel;

protected override void OnTreeFirstBuilt()

base.OnTreeFirstBuilt();

myPanel = new MyPanel();
myPanel.Parent = Panel;

Scaling

By default, ScreenPanels will rescaleall UI based on a 1080p target height automatically. If you wish to

disable this, or change the scaling to target the Desktop Resolution, you can change the following:

Create d 24 Se p 2024

Updated 28 Jun 2025 about

Razor Panels

UI can also be created using Razor, which allows you to use web-like HT ML/CSS to create and style each

Panel while also beingable to leverage C#.

The panels are created and rendered exactly the same way. They don't use a HT ML renderer. This syntax is

a convenience.

Creating a new PanelComponent

Every single UI consists of a PanelComponent at the root, with normal Panels being the children/content

within. The PanelComponent can be added to any GameObject that also has either a ScreenPanel or

WorldPanel component, and it will be drawn to whichever it has.

When you create a new Component, select "New Razor Panel Component" to get the following:

@using Sandbox;
@using Sandbox.UI;
@inherits PanelComponent

<root>

<div class="title">@MyStringValue</div>

</root>

@code

[Property, TextArea] public string MyStringValue { get; set; } = "Hello World!";

/// <summary>
/// the hash determines if the system should be rebuilt. If it changes, it will be
/// </summary>
protected override int BuildHash() => System.HashCode.Combine( MyStringValue );

HT ML/Razor

Anything within the <root> tags is treated as HT ML, allowing you to inject C# as-needed, like so:

<root>
 @foreach(var player in Player.All)

 <label>@player.Name</label>
 @if(player.IsDead)
 <img src="ui/skull.png" />
 </div>
</root>

If no <root> element is present, then any andall elements will be a child of your Panel's root

automatically.

You can also return early in Razor if you don't want it to render anything beyond the specified line.

BuildHash

A Panel's contents will only be rebuilt if the value returned from BuildHash() has changed from the previous

value, so make sure to include certain values here to ensure the Panel updates when necessary.

A Panel's contents will also rebuild if if has pointer-events and the cursor enters/exits/clicks the Panel.

You can also force a rebuild by calling StateHasChanged() . This will queue the rebuild for the next frame.

Creating a new Panel

Since a PanelComponent is the root, any child elements are instead Panels. These are created in the exact

same way PanelComponents are, but instead inheriting the Panel class (which .razor files do by default):

@using Sandbox;
@using Sandbox.UI;

<root>
 <div class="health">HP: @Health</div>
 <div class="armor">Armor: @Armor</div>
</root>

@code
 public int Health { get; set; } = 100;
 public int Armor { get; set; } = 100;

 protected override int BuildHash() => System.HashCode.Combine( Health, Armor );

How to Use

Back in your PanelComponent (or any other Panel), you can simply use the panel like any other element:

<MyChildPanel />

And can even pass variables to the Panel like so:

<MyChildPanel Health=@(30) Armor=@(75) />

How to store a Panel Ref erence

If you wish to store a reference to MyChildPanel so you can modify its properties in code, you can do this:

<root>
 <MyChildPanel @ref="PanelReference" />
</root>

@code
 MyChildPanel PanelReference { get; set; }

 protected override void OnStart()
 PanelReference.Health = Player.Local.Health;
 PanelReference.Armor = Player.Local.Armor;

T wo Way Binds

Sometimes you want to bind a variable to a control, and if it changes, sync the value back. That's what this

is.

You create a two way bind using :bind after the attribute name:

<SliderEntry min="0" max="100" step="1" Value:bind=@IntValue></SliderEntry>

@code

public int IntValue{ get; set; } = 32;

The example above will update the Slider when IntValue changes, and IntValue when the Slider changes

Dif f erences between Panel and PanelComponent

Since a Panel is not a Component, you cannot override OnStart , OnUpdate , ect.

Instead Panel has OnAfterTreeRender(bool firstTime) and Tick() .

Since PanelComponent is not a Panel, you have to access it's Panel via the PanelComponent.Panel

accessor.

This means where you can do Style.Left = Length.Auto on a Panel, you have to do

Panel.Style.Left = Length.Auto on a PanelComponent.

This also means you cannot do <MyPanelComponent /> within another Panel/PanelComponent, they must

be added to a GameObject with a ScreenPanel or WorldPanel.

Create d 24 Se p 2024

Updated 16 De c 2024 about

Razor Components

Razor Component allow you to define some content to show inside another razor file. This makes it easy to

create Panels that are more agile and reusable.

Creating a Razor Component

Here's an example called InfoCard.razor :

<root>
 <div class="header">@Header</div>
 <div class="body">@Body</div>
 <div class="footer">@Footer</div>
</root>

@code
 public RenderFragment Header { get; set; }
 public RenderFragment Body { get; set; }
 public RenderFragment Footer { get; set; }

Using a Razor Component

We can now very quickly and easily create Info Cards, and even add events/functions that interact with

the parent Panel:

<root>

<InfoCard>

 <Header>My Card</Header>
 <Body>
 <div class="title">This is my card</div>
 </Body>
 <Footer>
 <div class="button" onclick="@CloseCard">Close Card</div>
 </Footer>
 </InfoCard>
</root>

@code

 Delete();

Elements inside Panels

All Panels have a render fragment called ChildContent, so you can add elements inside of any Panel

without adding your own fragments:

<InfoCard>
 <ChildContent>
 <label>Something inside of InfoCard</label>
 </ChildContent>
</InfoCard>

Razor Components With Arguments

RenderFragment<T> is used to define a fragment that takes an argument. Here's PlayerList.razor :

@using Sandbox;

<root>
 @foreach ( var player in PlayerList )
 <div class="row">
 @PlayerRow( player )
 </div>
</root>

@code
 public List<Player> PlayerList { get; set; }
 public RenderFragment<Player> PlayerRow { get; set; }

As you can see, we're now defining PlayerRow which takes an argument. To call it we just call it like a

function, with the Player argument.

Now to use it we do this:

@using Sandbox;

<root>
 <PlayerList PlayerList=@MyPlayerList>
 <PlayerRow Context="item">
 @if (item is not Player player)
 return;

 <div class="row">@player.Health</div>
 </PlayerRow>
 </PlayerList>
</root>

@code
 List<Player> MyPlayerList;

In the PlayerRow, we add the special attribute Context , which tells our code generator that this is going to

need a special object context.

T hen in the fragment, we can convert this object into our target type. T hen you're free to use it as you

wish.

Generics

You can make a generic Panel class by using @typeparam to define the name of the parameter

@typeparam T

<root>
 This is my class for @Value
</root>

@code
 public T Value { get; set; }

You will then beable to use this like a regular generics class in C#, like PanelName<string> ect.

In Razor, you will need to add a T attribute to define the type like so:

<root>

<MyPanel T="string"></MyPanel>

</root>

Create d 24 Se p 2024

Updated 29 Aug 2025 about

Styling Panels

Using Stylesheets

It is common to have a file system like this:

Health.razor

Health.razor.scss

If you do this, the scss file is automatically included by your Health.razor panel.

If you want to specify a different location for the loaded Stylesheet, you can add this to your Panel class:

[StyleSheet("main.scss")]

You can also import a stylesheet from within another stylesheet like so:

@import "buttons.scss";

Styling Directly

T here are a few ways to style your Panels without a stylesheet. It's really recommended that you use a

stylesheet to keep things organized, but there are also valid reasons to use the following methods.

St yling t he Element

You can directly style any element just like you can in HT ML, but can inject C# when necessary:

<label style="color: red">DANGER!</label>
<div class="progress-bar">
 <div class="fill" style="width: @(Progress * 100f)%"></div>
</div>

St yle Block

Before or after your <root> element, you can add a <style> block that is read just like a Stylesheet:

 MyPanel {
 width: 100%;
 height: 100%;
 .hp { color: red; }
 .armor { color: blue; }
</style>

St yling in Code

You can a Panel's Style directly and modify the values however you'd like via Tick() or OnUpdate() :

myPanel.Style.Width = Length.Percent(Progress * 100f);

Create d 24 Se p 2024

Updated 25 Se p 2024 about

VirtualGrid

VirtualGrid is a Panel that allows you to create a grid of items virtually. What this means is that if you

have 1 million items, it won't render them and try to lay themall out at the same time. It'll just pick the few

that are visible and create them. When you scroll down, it'll delete the ones it can no longer see and create

the new visible ones.

Razor

You can use it in Razor like this

<VirtualGrid Items=@Items ItemSize=@(120)>
 <Item Context="item">
 @if (item is Package entry)

 <SpawnButton Icon="@entry.Thumb" Action="@(() => Spawn(entry))"></SpawnBut
 </Item>
</VirtualGrid>

@code
 public Package[] Items{ get; set; }

Here you can see that it sets the Items property (which takes any IEnumerable<T> ) and the ItemSize .

Item defines the cell contents. The cell has the class "cell" and will contain whatever you put in between

the <Item> elements.

ItemSize is a Vector2 . The cell size will be scaled up so it fits into the parent container flush. It'll keep the

aspect ratio of the ItemSize .

Gotchas

You need to make sure that VirtualGrid has a size in your styles. I usually make it width and height 100%.

All items obviously need to be the same size.

You can add spacing between elements using the gap styles on the VirtualGrid element.

Create d 30 Aug 2025

Updated 30 Aug 2025