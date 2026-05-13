 about

Raw Input

We very much recommend that you only use this if you can't use input actions for whatever

reason. You can't rebind these atall.

We have the ability to access keyboard inputs directly, bypassing input actions.

// Is the W key down this frame?
if ( Input.Keyboard.Down( "W" ) )
 Log.Info( "W is down!" );

// Was the W key pressed this frame?
if ( Input.Keyboard.Pressed( "W" ) )
 Log.Info( "W was pressed!" );

// Was the W key released this frame?
if ( Input.Keyboard.Released( "W" ) )
 Log.Info( "W was released!" );

Most of the keys on the keyboard should work, here's an exhaustive list of them.

Ke y

Na me

"0" - "9"

"a" - "z"

"KP_0" - "KP_9"

"KP_DIVIDE"

0 - 9

A - Z

Numpad 0 - Numpad 9

Numpad /

Na me

"KP_MULTIPLY"

"KP_MINUS"

"KP_PLUS"

"KP_ENTER"

"KP_DEL"

"SEMICOLON"

"ENTER"

"SPACE"

"BACKSPACE"

"TAB"

"CAPSLOCK"

"NUMLOCK"

"ESCAPE"

"SCROLLLOCK"

"INS"

"DEL"

"HOME"

"END"

Numpad *

Numpad -

Numpad +

Numpad Enter

Numpad Delete

Less Than

More Than

Left Bracket

Right Bracket

Semicolon

Apostrophe

Backtick / Console Key

Comma

Period

Slash

Backslash

Hyphen / Minus

Equals

Enter

Space

Backspace

Tab

Caps Lock

Num Lock

Escape

Scroll Lock

Insert

Delete

Home

End

Na me

Page Up

Page Down

Pause

Left Shift

Right Shift

Left Alt

Right Alt

Up Arrow

Left Arrow

Right Arrow

Down Arrow

"PGUP"

"PGDN"

"PAUSE"

"SHIFT"

"RSHIFT"

"ALT"

"RALT"

"UPARROW"

"LEFTARROW"

"RIGHTARROW"

"DOWNARROW"

Create d 7 Apr 2025

Updated 15 May 2025