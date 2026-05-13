 about

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

Updated 15 Jun 2025