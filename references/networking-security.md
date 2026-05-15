# Networking And Security

s&box multiplayer work should be host-authoritative by default.

## Authority

- Treat clients as input providers, not truth sources.
- Run meaningful game-state changes on the host.
- Use `Networking.IsHost` or `!IsProxy` before spawning, destroying, awarding money, applying damage, changing inventory, saving data, or modifying shared resources.
- Validate `Rpc.Caller`, ownership, distance, cooldowns, costs, permissions, and object validity on the host.

## RPC And Sync

- Use `[Sync]` for replicated state that clients need to render or predict.
- Use `[Sync( SyncFlags.FromHost )]` when only host-authored state should replicate.
- Use `[Rpc.Host]` for client requests. Validate inside the method before doing anything.
- Use `[Rpc.Broadcast]` for effects or events that all clients should see after host approval.
- Use owner-only or host-only flags when the local project uses them and the event should be restricted.

## Secure Component Template

```csharp
public sealed class DoorLock : Component
{
	[Property] public float UseDistance { get; set; } = 96f;

	[Sync( SyncFlags.FromHost )]
	public bool IsLocked { get; private set; }

	[Rpc.Host]
	public void RequestSetLocked( bool locked )
	{
		if ( !Networking.IsHost ) return;
		if ( !CanCallerUseThis() ) return;

		IsLocked = locked;
		PlayLockChangedEffects( locked );
	}

	bool CanCallerUseThis()
	{
		var caller = Rpc.Caller;
		if ( caller is null ) return false;

		var player = Player.FindForConnection( caller );
		if ( !player.IsValid() ) return false;

		var distance = player.Transform.World.Position.Distance( Transform.World.Position );
		if ( distance > UseDistance ) return false;

		// Add game-specific ownership, job, admin, money, cooldown, or inventory checks here.
		return true;
	}

	[Rpc.Broadcast]
	private void PlayLockChangedEffects( bool locked )
	{
		// Visual/audio feedback only. Do not put authoritative state changes here.
		Sound.Play( locked ? "sounds/lock.sound" : "sounds/unlock.sound", Transform.World.Position );
	}
}
```

Rules from the template:

- `RequestSetLocked` is the only client entrypoint and runs on host.
- `IsLocked` is host-authored replicated state.
- `PlayLockChangedEffects` is feedback only; clients do not decide state.
- `CanCallerUseThis` is where project-specific security lives.

## Networked Objects

- Spawn networked objects from the host.
- Assign owners deliberately with `NetworkSpawn( owner )` or project-established spawn helpers.
- Use fixed ownership when the object should not transfer.
- Mark purely local visual/post-process helper objects as not networked when possible.
- Refresh network state only when needed and only through public supported APIs.

## Ownership Patterns

- Add or reuse an ownership/access component for player-spawned objects.
- Host/admin may be exempt when the game rules require it.
- For toolgun/physgun/editor actions, validate both the caller and the target object.
- Never let client UI directly mutate authoritative inventory, money, job, or permission state.

## Anti-Patterns

- Do not trust object references sent by clients without validity and access checks.
- Do not run server-only logic on proxies.
- Do not use reflection or private engine calls to force network/editor behavior.
- Do not hide security in UI state; UI can lie.
