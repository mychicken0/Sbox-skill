# Physics And Traces

Use local project examples first; trace masks/tags vary by game.

## Scene Trace Pattern

```csharp
var tr = Scene.Trace
	.Ray( start, end )
	.IgnoreGameObjectHierarchy( GameObject )
	.WithoutTags( "trigger" )
	.Run();

if ( tr.Hit )
{
	var hitObject = tr.GameObject;
	var hitComponent = hitObject?.Components.Get<MyComponent>();
}
```

Some projects use `Game.SceneTrace`. Match the local project API surface.

## Rigidbody And Physics

```csharp
var rb = GameObject.Components.Get<Rigidbody>();
if ( !rb.IsValid() || rb.IsProxy ) return;

rb.Velocity += impulse;
```

Host should own physical gameplay changes when state matters.

## Collision Listener

```csharp
public sealed class Projectile : Component, Component.ICollisionListener
{
	void Component.ICollisionListener.OnCollisionStart( Collision collision )
	{
		if ( !Networking.IsHost ) return;
		if ( collision.Other.GameObject is null ) return;
	}
}
```

## Trigger Listener

```csharp
public sealed class TriggerZone : Component, Component.ITriggerListener
{
	void Component.ITriggerListener.OnTriggerEnter( Collider other )
	{
		if ( !Networking.IsHost ) return;
	}
}
```

## Damage Pattern

```csharp
var damageable = target.GetComponent<Component.IDamageable>();
if ( damageable is null ) return;

var dmg = new DamageInfo( amount, attacker, weapon );
damageable.OnDamage( in dmg );
```

## Safety

- Validate object validity after awaits, delayed tasks, and network calls.
- Ignore self and owner hierarchies in traces when appropriate.
- Keep physics mutation out of proxies.
- Use tags consistently; do not invent tags without checking project usage.
