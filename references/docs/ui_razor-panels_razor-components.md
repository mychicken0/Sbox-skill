 about

Razor Components

Razor Component allow you to define some content to show inside another razor file. This makes it easy to

create Panels that are more agile and reusable.

Creating a Razor Component

Here's an example called InfoCard.razor :

<root>
 <div class="header">@Header</div>
 <div class="body">@Body</div>
 <div class="footer">@Footer</div>
</root>

@code
 public RenderFragment Header { get; set; }
 public RenderFragment Body { get; set; }
 public RenderFragment Footer { get; set; }

Using a Razor Component

We can now very quickly and easily create Info Cards, and even add events/functions that interact with

the parent Panel:

<root>

<InfoCard>

 <Header>My Card</Header>
 <Body>
 <div class="title">This is my card</div>
 </Body>
 <Footer>
 <div class="button" onclick="@CloseCard">Close Card</div>
 </Footer>
 </InfoCard>
</root>

@code

 Delete();

Elements inside Panels

All Panels have a render fragment called ChildContent, so you can add elements inside of any Panel

without adding your own fragments:

<InfoCard>
 <ChildContent>
 <label>Something inside of InfoCard</label>
 </ChildContent>
</InfoCard>

Razor Components With Arguments

RenderFragment<T> is used to define a fragment that takes an argument. Here's PlayerList.razor :

@using Sandbox;

<root>
 @foreach ( var player in PlayerList )
 <div class="row">
 @PlayerRow( player )
 </div>
</root>

@code
 public List<Player> PlayerList { get; set; }
 public RenderFragment<Player> PlayerRow { get; set; }

As you can see, we're now defining PlayerRow which takes an argument. To call it we just call it like a

function, with the Player argument.

Now to use it we do this:

@using Sandbox;

<root>
 <PlayerList PlayerList=@MyPlayerList>
 <PlayerRow Context="item">
 @if (item is not Player player)
 return;

 <div class="row">@player.Health</div>
 </PlayerRow>
 </PlayerList>
</root>

@code
 List<Player> MyPlayerList;

In the PlayerRow, we add the special attribute Context , which tells our code generator that this is going to

need a special object context.

T hen in the fragment, we can convert this object into our target type. T hen you're free to use it as you

wish.

Generics

You can make a generic Panel class by using @typeparam to define the name of the parameter

@typeparam T

<root>
 This is my class for @Value
</root>

@code
 public T Value { get; set; }

You will then beable to use this like a regular generics class in C#, like PanelName<string> ect.

In Razor, you will need to add a T attribute to define the type like so:

<root>

<MyPanel T="string"></MyPanel>

</root>

Create d 24 Se p 2024

Updated 29 Aug 2025