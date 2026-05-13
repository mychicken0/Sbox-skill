 about

Razor Panels

UI can also be created using Razor, which allows you to use web-like HT ML/CSS to create and style each

Panel while also beingable to leverage C#.

The panels are created and rendered exactly the same way. They don't use a HT ML renderer. This syntax is

a convenience.

Creating a new PanelComponent

Every single UI consists of a PanelComponent at the root, with normal Panels being the children/content

within. The PanelComponent can be added to any GameObject that also has either a ScreenPanel or

WorldPanel component, and it will be drawn to whichever it has.

When you create a new Component, select "New Razor Panel Component" to get the following:

@using Sandbox;
@using Sandbox.UI;
@inherits PanelComponent

<root>

<div class="title">@MyStringValue</div>

</root>

@code

[Property, TextArea] public string MyStringValue { get; set; } = "Hello World!";

/// <summary>
/// the hash determines if the system should be rebuilt. If it changes, it will be
/// </summary>
protected override int BuildHash() => System.HashCode.Combine( MyStringValue );

HT ML/Razor

Anything within the <root> tags is treated as HT ML, allowing you to inject C# as-needed, like so:

<root>
 @foreach(var player in Player.All)

 <label>@player.Name</label>
 @if(player.IsDead)
 <img src="ui/skull.png" />
 </div>
</root>

If no <root> element is present, then any andall elements will be a child of your Panel's root

automatically.

You can also return early in Razor if you don't want it to render anything beyond the specified line.

BuildHash

A Panel's contents will only be rebuilt if the value returned from BuildHash() has changed from the previous

value, so make sure to include certain values here to ensure the Panel updates when necessary.

A Panel's contents will also rebuild if if has pointer-events and the cursor enters/exits/clicks the Panel.

You can also force a rebuild by calling StateHasChanged() . This will queue the rebuild for the next frame.

Creating a new Panel

Since a PanelComponent is the root, any child elements are instead Panels. These are created in the exact

same way PanelComponents are, but instead inheriting the Panel class (which .razor files do by default):

@using Sandbox;
@using Sandbox.UI;

<root>
 <div class="health">HP: @Health</div>
 <div class="armor">Armor: @Armor</div>
</root>

@code
 public int Health { get; set; } = 100;
 public int Armor { get; set; } = 100;

 protected override int BuildHash() => System.HashCode.Combine( Health, Armor );

How to Use

Back in your PanelComponent (or any other Panel), you can simply use the panel like any other element:

<MyChildPanel />

And can even pass variables to the Panel like so:

<MyChildPanel Health=@(30) Armor=@(75) />

How to store a Panel Ref erence

If you wish to store a reference to MyChildPanel so you can modify its properties in code, you can do this:

<root>
 <MyChildPanel @ref="PanelReference" />
</root>

@code
 MyChildPanel PanelReference { get; set; }

 protected override void OnStart()
 PanelReference.Health = Player.Local.Health;
 PanelReference.Armor = Player.Local.Armor;

T wo Way Binds

Sometimes you want to bind a variable to a control, and if it changes, sync the value back. That's what this

is.

You create a two way bind using :bind after the attribute name:

<SliderEntry min="0" max="100" step="1" Value:bind=@IntValue></SliderEntry>

@code

public int IntValue{ get; set; } = 32;

The example above will update the Slider when IntValue changes, and IntValue when the Slider changes

Dif f erences between Panel and PanelComponent

Since a Panel is not a Component, you cannot override OnStart , OnUpdate , ect.

Instead Panel has OnAfterTreeRender(bool firstTime) and Tick() .

Since PanelComponent is not a Panel, you have to access it's Panel via the PanelComponent.Panel

accessor.

This means where you can do Style.Left = Length.Auto on a Panel, you have to do

Panel.Style.Left = Length.Auto on a PanelComponent.

This also means you cannot do <MyPanelComponent /> within another Panel/PanelComponent, they must

be added to a GameObject with a ScreenPanel or WorldPanel.

Create d 24 Se p 2024

Updated 16 De c 2024