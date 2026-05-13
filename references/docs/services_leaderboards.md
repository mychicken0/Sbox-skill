 about

Leaderboards

Leaderboards are just stats, aggregated and ordered.

Basic Example

Here's how to get a leaderboard. We want to get a leaderboard to show who has killed the most zombies,

globally.

var board = Sandbox.Services.Leaderboards.GetFromStat( "facepunch.ss1", "zombies_kille
await board.Refresh();

foreach ( var entry in board.Entries )

Log.Info( $"{entry.Rank} - {entry.DisplayName} - {entry.Value}" );

By default, leaderboards are aggregated using the sum ofall the stats and ordered descending.

By Country

You can filter a leaderboard by country. This will only show stats that were created in that country.

var board = Sandbox.Services.Leaderboards.GetFromStat( "facepunch.ss1", "zombies_kille
board.SetCountryCode( "gb" );
await board.Refresh();

foreach ( var entry in board.Entries )

Log.Info( $"{entry.Rank} - {entry.DisplayName} - {entry.Value} [{entry.CountryCode

By Date

If you pass countrycode as "auto" it will use the current player's location

You can filter leaderboards by date, allowing yearly, weekly, monthly or daily leaderboards.

board.FilterByMonth();
board.SetDatePeriod( new System.DateTime( 2024, 8, 1 ) );
await board.Refresh();

foreach ( var entry in board.Entries )

Log.Info( $"{entry.Rank} - {entry.DisplayName} - {entry.Value} [{entry.CountryCode

If you don't set a date period, it'll use the current date

Centering

You can focus the leaderboard on a certain player. This will show the results around that player. It is nice to

show a player's contemperies rather than showing the top 20all the time.

var board = Sandbox.Services.Leaderboards.GetFromStat( "facepunch.ss1", "zombies_kille
board.CenterOnSteamId( 76561197960279927 );
await board.Refresh();

foreach ( var entry in board.Entries )

Log.Info( $"{entry.Rank} - {entry.DisplayName} - {entry.Value}" );

You can also call .CenterOnMe() to center on the local player.

Aggregation and Sorting

So maybe instead of the sum of something, we want to show people's shortest result. Like in this example,

we're showing a list of the fastest win times.

var board = Sandbox.Services.Leaderboards.GetFromStat( "facepunch.ss1", "victory_elaps

board.SetAggregationMin(); // select the lowest value from each player
board.SetSortAscending(); // order by the lowest value first
board.FilterByMonth(); // only show results from this month
board.CenterOnMe(); // offset so I'm in the middle of the results
board.MaxEntries = 100;

await board.Refresh();

foreach ( var entry in board.Entries )

Log.Info( $"{entry.Rank} - {entry.DisplayName} - {entry.Value} [{entry.Timestamp}]

The entry timestamp holds the time of the selected result

Create d 23 Aug 2024

Updated 23 Aug 2024