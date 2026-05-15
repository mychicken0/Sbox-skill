# Core API Reference

This is a compact practical reference, not a complete API dump. Use local project code and official docs when a member is missing or version-sensitive.

## `Component`

```csharp
public abstract class Component
{
	public GameObject GameObject { get; }
	public Scene Scene { get; }
	public Transform Transform { get; }
	public bool Enabled { get; set; }
	public bool IsProxy { get; }
	public NetworkComponent Network { get; }
	public GameTags Tags { get; }

	protected virtual void OnAwake() {}
	protected virtual void OnStart() {}
	protected virtual void OnEnabled() {}
	protected virtual void OnDisabled() {}
	protected virtual void OnUpdate() {}
	protected virtual void OnFixedUpdate() {}
	protected virtual void OnDestroy() {}

	public T GetComponent<T>();
	public T GetComponentInChildren<T>( bool includeDisabled = false );
	public T GetComponentInParent<T>( bool includeDisabled = false );

	public interface ICollisionListener {}
	public interface ITriggerListener {}
	public interface IDamageable {}
	public interface INetworkListener {}
}
```

Common usage:

```csharp
if ( !Networking.IsHost ) return;
if ( !this.IsValid() || IsProxy ) return;
```

## `GameObject`

```csharp
public sealed class GameObject
{
	public string Name { get; set; }
	public bool Enabled { get; set; }
	public bool IsProxy { get; }
	public bool IsDestroyed { get; }
	public Scene Scene { get; }
	public Transform Transform { get; }
	public ComponentList Components { get; }
	public GameTags Tags { get; }
	public NetworkAccessor Network { get; }
	public GameObjectFlags Flags { get; set; }
	public string PrefabInstanceSource { get; }

	public GameObject( bool enabled = true, string name = null );

	public void SetParent( GameObject parent );
	public T GetOrAddComponent<T>() where T : Component;
	public void Destroy();
	public void NetworkSpawn( Connection owner = null );
	public void NetworkSpawn( bool recursive, Connection owner = null );

	public static GameObject Clone( PrefabFile prefab, CloneConfig config = default );
	public static GameObject Clone( string prefabPath, CloneConfig config = default );
}
```

Common usage:

```csharp
var go = new GameObject( true, "Thing" );
var comp = go.AddComponent<MyComponent>();
var clone = GameObject.Clone( prefab, new CloneConfig { Name = "Spawned", Transform = transform } );
clone.NetworkSpawn( owner );
```

## `Scene`

```csharp
public sealed class Scene
{
	public CameraComponent Camera { get; }
	public SceneTrace Trace { get; }

	public T Get<T>() where T : class;
	public IEnumerable<T> GetAll<T>();
	public IEnumerable<T> GetAllComponents<T>();
	public void RunEvent<T>( Action<T> action );
}
```

Common usage:

```csharp
var manager = Scene.Get<MySystem>();
foreach ( var component in Scene.GetAllComponents<MyComponent>() ) {}

var tr = Scene.Trace.Ray( start, end ).Run();
```

## `GameObjectSystem<T>`

```csharp
public abstract class GameObjectSystem<T>
{
	public static T Current { get; }
	public Scene Scene { get; }

	protected GameObjectSystem( Scene scene );
}
```

Common usage:

```csharp
public sealed class InventorySystem : GameObjectSystem<InventorySystem>
{
	public InventorySystem( Scene scene ) : base( scene ) {}
}
```

## `PanelComponent`

```csharp
public abstract class PanelComponent : Component
{
	public Panel Panel { get; }

	protected virtual int BuildHash();
	protected void StateHasChanged();
}
```

Common usage:

```razor
@inherits PanelComponent

@code
{
	protected override int BuildHash() => HashCode.Combine( IsOpen, Count );
}
```

## `Time`

```csharp
public static class Time
{
	public static float Delta { get; }
	public static float Now { get; }
	public static float FixedDelta { get; }
	public static float Scale { get; set; }
}

public struct TimeSince
{
	public static implicit operator float( TimeSince value );
}

public struct TimeUntil
{
	public static implicit operator float( TimeUntil value );
}
```

Common usage:

```csharp
Position += Velocity * Time.Delta;

TimeSince lastUsed = 0;
if ( lastUsed > 1.0f ) {}

TimeUntil explodeIn = 3.0f;
if ( explodeIn <= 0 ) {}
```
