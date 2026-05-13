 about

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

Updated 23 O ct 2025