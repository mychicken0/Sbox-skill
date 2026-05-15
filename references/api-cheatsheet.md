# API Cheatsheet

Use this as a quick memory jogger. Still inspect local code first because projects wrap these APIs differently.

## Components

```csharp
public sealed class MyComponent : Component
{
	[Property] public GameObject Target { get; set; }
	[Property, Range( 0, 100 )] public float Strength { get; set; } = 10f;

	protected override void OnStart() {}
	protected override void OnUpdate() {}
	protected override void OnFixedUpdate() {}
	protected override void OnDestroy() {}
}
```

Common access:

```csharp
var component = GameObject.Components.Get<MyComponent>( FindMode.EnabledInSelfAndDescendants );
var created = GameObject.GetOrAddComponent<MyComponent>();
foreach ( var item in Scene.GetAllComponents<MyComponent>() ) {}
```

## Scene Systems

```csharp
public sealed class MySystem : GameObjectSystem<MySystem>
{
	public MySystem( Scene scene ) : base( scene ) {}
}
```

Use systems for scene-wide coordination. Do not use static global state when the scene system should own it.

## GameObjects And Prefabs

```csharp
var go = new GameObject( true, "Readable Name" );
var child = new GameObject( true, "Child" );
child.SetParent( go );

var clone = GameObject.Clone( prefab, new CloneConfig
{
	Name = "Spawned Thing",
	StartEnabled = false,
	Transform = transform
} );
```

## Validity And Guards

```csharp
if ( !component.IsValid() ) return;
if ( GameObject.IsDestroyed ) return;
if ( IsProxy ) return;
if ( !Networking.IsHost ) return;
```

## Common Attributes

```csharp
[Title( "Nice Name" )]
[Category( "Gameplay" )]
[Icon( "bolt" )]
[Property, Group( "Tuning" ), Range( 0, 1 ), Step( 0.01f )]
public float Value { get; set; }
```

## Time Helpers

Use `Time.Delta` for frame-scaled changes. Use `TimeSince` and `TimeUntil` for timers when the local project already uses them.
