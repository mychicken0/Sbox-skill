 about

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

Updated 19 Nov 2025