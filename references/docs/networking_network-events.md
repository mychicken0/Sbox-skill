 about

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

Updated 13 Mar 2024