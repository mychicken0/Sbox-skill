 about

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

Updated 9 Se p 2024