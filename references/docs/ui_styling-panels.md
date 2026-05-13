 about

Styling Panels

Using Stylesheets

It is common to have a file system like this:

Health.razor

Health.razor.scss

If you do this, the scss file is automatically included by your Health.razor panel.

If you want to specify a different location for the loaded Stylesheet, you can add this to your Panel class:

[StyleSheet("main.scss")]

You can also import a stylesheet from within another stylesheet like so:

@import "buttons.scss";

Styling Directly

T here are a few ways to style your Panels without a stylesheet. It's really recommended that you use a

stylesheet to keep things organized, but there are also valid reasons to use the following methods.

St yling t he Element

You can directly style any element just like you can in HT ML, but can inject C# when necessary:

<label style="color: red">DANGER!</label>
<div class="progress-bar">
 <div class="fill" style="width: @(Progress * 100f)%"></div>
</div>

St yle Block

Before or after your <root> element, you can add a <style> block that is read just like a Stylesheet:

 MyPanel {
 width: 100%;
 height: 100%;
 .hp { color: red; }
 .armor { color: blue; }
</style>

St yling in Code

You can a Panel's Style directly and modify the values however you'd like via Tick() or OnUpdate() :

myPanel.Style.Width = Length.Percent(Progress * 100f);

Create d 24 Se p 2024

Updated 25 Se p 2024