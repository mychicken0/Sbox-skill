 about

Using With C#

Here's how you can use ActionGraph with your game code written in C#.

public class ExampleComponent : Component

[Property]
public Action ExampleAction { get; set; }

protected override void OnUpdate()

if ( Input.Down( "attack1" ) )

ExampleAction?.Invoke();

Declaring the Property

[Property]
public Action ExampleAction { get; set; }

This will add a property that we can see in the inspector. For a property to be usable as an ActionGraph it

must have a Delegate type. We're using the type Action here, which takes in no parameters and returns

nothing. Once we do this we can press the "+" to add as many callbacks to the Action as we want.

will show only the one action in-line without having the option to add/remove others.

Clicking on the Example Action or Empty Action will open the ActionGraph editor and start editing it.

Adding Paramet ers

If you want to beable to pass in some parameters, you can use a different delegate type:

[Property]
public Action<int, string, GameObject> ExampleAction { get; set; }

declared them.

Renaming Paramet ers

T here's a couple of ways to rename the parameters, since "Arg 1", "Arg 2" isn't very helpful. First, you can

click on the root node in the editor, and change the socket names and descriptions in the Properties panel.

The other way is to use a custom delegate type:

public delegate void ExampleDelegate( int someNumber, string someText, GameObject some

[Property]
public ExampleDelegate ExampleAction { get; set; }

This will automatically fill in the names of each parameter like above, and you can re-use the same

delegate type for any property that would take in the same set of parameters.

Running an ActionGraph

You can call the property like any other method directly:

ExampleAction();

However, if the action hasn't been created in the editor yet, this will throw a NullReferenceException . A

safer way to run it is to check for null like this:

This is shorthand for:

if ( ExampleAction is not null ) ExampleAction();

Passing in Argument s

If you've declared some parameters, you can pass in values when running the graph like this:

ExampleAction( 123, "Hello, World!", GameObject.Parent );

Or if you're checking for null:

ExampleAction?.Invoke( 123, "Hello, World!", GameObject.Parent );

Ret urning Values

Delegates with return types are supported too.

[Property]
public Func<int> TestExpression { get; set; }

Graphs implementing delegates like this will have an Output node, which you'll need to connect to the

input without going through any async nodes (like delays).

Async Graphs

If you want to wait for a graph with delays to finish running, it needs to be declared with a delegate type

that returns a T ask.

[Property]
public Func<Task> ExampleAction { get; set; }

With parameters:

[Property]
public Func<int, string, GameObject, Task> ExampleAction { get; set; }

public delegate Task ExampleDelegate( int someNumber, string someText, GameObject some

[Property]
public ExampleDelegate ExampleAction { get; set; }

When you call it you can either await the returned task, or use ContinueWith outside of async code.

await ExampleAction( 123, "Hello, World!", GameObject.Parent );

ExampleAction?.Invoke( 123, "Hello, World!", GameObject.Parent )
 .ContinueWith( task => { } );

Next Steps

T ake a look at the Intro to ActionGraphs guide to learn how to edit your new graph.

Create d 8 Jan 2024

Updated 2 Jun 2025