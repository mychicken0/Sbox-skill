 about

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

Updated 30 O ct 2024