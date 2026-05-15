# Razor UI And SCSS

Use Razor panels for gameplay UI that should be quick to read, quick to act on, and easy to dismiss.

## Panel Structure

- Use `.razor` plus matching `.razor.scss`.
- Prefer `PanelComponent` when the panel needs component lifecycle, input polling, or scene access.
- Render nothing when closed or missing required data.
- Keep UI state local; send authoritative actions through validated component/system methods or RPCs.
- Implement `BuildHash` when state changes should drive efficient rerendering.

## Razor Boilerplate

```razor
@using Sandbox;
@using Sandbox.UI;
@namespace Sandbox
@inherits PanelComponent

@if ( !IsOpen )
	return;

<root>
	<div class="backdrop" onclick="@Close"></div>

	<div class="window">
		<div class="header">
			<div class="title">PANEL TITLE</div>
			<button class="close" onclick="@Close">Close</button>
		</div>

		<div class="content">
			<button class="primary" onclick="@OnPrimaryClicked">Do Thing</button>
		</div>
	</div>
</root>

@code
{
	public bool IsOpen { get; private set; }
	int _version;

	protected override void OnUpdate()
	{
		if ( Input.Pressed( "Menu" ) )
		{
			if ( IsOpen ) Close();
			else Open();
		}

		if ( IsOpen && Input.EscapePressed )
		{
			Close();
			Input.EscapePressed = false;
		}
	}

	protected override int BuildHash()
	{
		return HashCode.Combine( IsOpen, _version );
	}

	void Open()
	{
		IsOpen = true;
		_version++;
		StateHasChanged();
	}

	void Close()
	{
		IsOpen = false;
		_version++;
		StateHasChanged();
	}

	void OnPrimaryClicked()
	{
		// Call a local component method or validated RPC; do not trust UI state.
		_version++;
		StateHasChanged();
	}
}
```

Matching SCSS:

```scss
MyPanel {
	position: absolute;
	inset: 0;
	pointer-events: none;
}

.backdrop {
	position: absolute;
	inset: 0;
	background-color: rgba(0, 0, 0, 0.45);
	pointer-events: all;
}

.window {
	pointer-events: all;
}

button {
	pointer-events: all;
}
```

## Input And Interaction

- s&box panels are non-interactive by default. Any clickable/drag/input surface must have `pointer-events: all` in SCSS.
- Stop event propagation for item clicks, drags, context menus, and modal interactions where backdrop handling exists.
- Use explicit local drag/hover/context state; validate final actions on the server.
- Support fast close paths such as Escape or backdrop click when appropriate.

## SCSS

- Define local tokens for panel background, borders, text, accent, success, warning, and danger.
- Use restrained styling for in-game tools: clear hierarchy, readable text, minimal decoration.
- Avoid generic web dashboard patterns for diegetic/gameplay UI.
- Use stable dimensions for grids, slots, toolbars, counters, and repeated controls.
- Make labels fit: use ellipsis, wrapping, or fixed bounds so text does not overlap.

## Good Defaults

- Use `pointer-events: none` on full-screen root overlays, then enable interaction on windows/buttons/inputs.
- Keep transitions short and functional.
- Use `sound-in` hover/select only when the project already uses UI sounds.
- Avoid blocking gameplay visibility more than necessary.
