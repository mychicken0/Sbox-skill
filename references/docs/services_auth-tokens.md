 about

Auth Tokens

If you are using HT T P requests or WebSockets in your game, you can use Auth T okens to validate that the

requests were sent from a valid Steam user in a s&box game session. This is useful if you want to tie data

to a specific Steam account, or prevent botting.

Generating Tokens

You can generate a new token with Sandbox.Services like so:

var token = await Sandbox.Services.Auth.GetToken( "YourServiceName" );

Validating Tokens

To validate a token on your backend, you need to make a call to the services.facepunch.com/sbox API

using the auth/token endpoint.

Here is an example of how to validate a token in C# using System.Net.Http

private class ValidateAuthTokenResponse

public long SteamId { get; set; }
public string Status { get; set; }

public static async Task<bool> ValidateToken( long steamId, string token )

var http = new System.Net.Http.HttpClient();
var data = new Dictionary<string, object>

{ "steamid", steamId },
{ "token", token }

var content = new StringContent( JsonSerializer.Serialize( data ), Encoding.UTF8,
var result = await http.PostAsync( "https://services.facepunch.com/sbox/auth/token

if ( result.StatusCode != HttpStatusCode.OK ) return false;

var response = await result.Content.ReadFromJsonAsync<ValidateAuthTokenResponse>()
if ( response is null || response.Status != "ok" ) return false;

At some point when receiving the token from the client on your backend you can then validate it as such:

var isValidToken = await ValidateToken( steamId, token );

if ( isValidToken )

Console.WriteLine( "Success!" );

Create d 22 De c 2023

Updated 14 Aug 2025