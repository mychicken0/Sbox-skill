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
@using System;
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

## Text Rendering Quirks (s&box-specific)

s&box's Razor/SCSS renderer does **not** behave like a browser. Text layout clips content in ways that standard CSS properties cannot fix. These are proven workarounds:

### Problem: Text Bottom Clipping ("Sinking Text")

The renderer calculates element height from `font-size` alone and ignores glyph descenders (`y`, `g`, `p`, `q`, `j`), causing the bottom pixels of text to be cut off.

**What does NOT work in s&box:**
- `overflow: visible` - s&box ignores this; elements clip their children regardless.
- `line-height: 1.6` or higher - has no effect on the calculated element height.

**What DOES work:**
1. **Set explicit `height` on the text row** (e.g., `height: 28px` for `font-size: 13px`). This forces the renderer to allocate enough vertical space.
2. **Add `padding-bottom: 6px`** to every element that contains text. This pushes the bottom boundary below the descender line.
3. **Use `align-items: flex-start`** instead of `center` on flex rows containing text. Centering causes both top and bottom to be clipped equally.

**Example (correct):**
```scss
.hud-row {
    height: 28px;
    flex-direction: row;
    align-items: flex-start;
    font-size: 13px;

    .hud-label {
        padding-bottom: 6px;
    }
    .hud-value {
        padding-bottom: 6px;
    }
}
```

### Problem: Namespace Resolution in Razor `@code` Blocks

Razor `.razor` files do not auto-import `System`. Using `Math.Clamp`, `Math.Round`, or other `System` types in `@code {}` blocks will produce `CS0103` errors.

**Fix:** Always add `@using System;` at the top of Razor files that use standard library types in code blocks.

### Problem: Special Characters / Non-ASCII Glyphs

Monospace fonts in s&box may not render special Unicode characters (for example, a degree symbol) correctly. They can cause layout wrapping or display as garbled text when the glyph width differs from the monospace grid.

**Fix:** Use plain ASCII equivalents such as `C`, `deg`, or `TEMP C` for HUD/terminal-style displays.

### General SCSS Tips for s&box

- Prefer `padding` over `margin` for spacing - margin collapse behaves unpredictably.
- Use fixed `width` on containers rather than relying on flex auto-sizing.
- Avoid `gap` in flex layouts when precise control is needed; use `margin-right` on children instead.
- Always test text rendering in-engine; the s&box editor preview may differ from runtime rendering.
