 about

Http Requests

s&box provides a static Http class, this lets you easily create asynchronous HT T P requests of different

methods (GET , POST , DELET E, etc…) providing JSON content and parsing JSON responses.

Allowed URLs

You can only use http or https URLs to domains (no IP addresses), and to prevent abuse, localhost is

permitted only on ports 80/443/8080/8443.

The command line switch -allowlocalhttp will let you access any local URL from the server.

Cheat Sheet

Some common things you might want to do…

// GET request that returns the response as a string
string response = await Http.RequestStringAsync( "https://google.com" );

// POST request of JSON content ignoring any response
await Http.RequestAsync( "https://api.facepunch.com/my/method", "POST", Http.CreateJso

Create d 26 Se p 2024

Updated 26 Se p 2024