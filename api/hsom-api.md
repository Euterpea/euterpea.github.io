# HSoM API

This page gives a list of important datatypes and functions in the HSoM library. 
For more information on the functions, types, and type classes listed here, please see the Haskell School of 
Music textbook or, from GHCi with Euterpea and HSoM imported, type the following:

``:i nameYouWantToKnowAbout``

## Performance Functions and Type Classes

| Function/Class	| Description |
| ----- | ----- |
| hsomPerform	| Player-based conversion from Music to Performance. |
| Performable	| Type class with one function, perfDur, for performance with players. |
| playA	| Like Euterpea's play but for use with HSoM's Players. |
| writeMidiA	| Like Euterpea's writeMidi, but for use with HSoM's Players. |

## UISF Functions and Widgets

| Function	| Description |
| ----- | ----- |
| button	| Button widget. |
| checkbox	| Checkbox widget. |
| checkGroup	| Collection of check box widgets. |
| defaultMUIParams	| Default Window parameters for use with runMUI. |
| display	| Display a value (requires a Show instance). |
| displayStr	| Display a String without quotes. |
| getTime	| Time since program start in milliseconds. |
| hSlider / hiSlider	| Horizontal slider for continuous/discrete values. |
| label	| Text label. |
| leftRight / rightLeft	| Widgets get added from left to right or right to left. |
| listbox	| List box widget. |
| radio	| Collection of radio button widgets. |
| runMUI	| Run a UISF Window using the UIParams (like defaultMUIParams). |
| runMUI'	| Like runMUI but without the UIParams argument. |
| setLayout	| Set window layout. |
| setSize	| Set the window size. |
| stickyButton	| Button that stays depressed when clicked and must be clicked again to release it. |
| textbox	| Textbox widget that allows user input. |
| title	| Set the title of a window. |
| topDown/bottomUp	| Widgets get added from top to bottom or bottom to top. |
| vSlider/viSlider	| Vertical slider for continuous/discrete values. |
| withDisplay	| Attach a display to a value. |

## MIDI Widgets

| Function	| Description |
| ----- | ----- |
| selectInput	| Select a MIDI input device. |
| midiIn	| Receive from a MIDI input device. |
| midiInM	| Receive from multiple MIDI input devices. |
| midiOut	| Receive from a MIDI output device. |
| midiOutB	| Send buffered, time-stamped events to a single MIDI output device. |
| midiOutM	| Send to multiple MIDI output devices. |
| midiOutMB	| Send buffered, time-stamped events to multiple MIDI output devices. |
| selectInputM	| Select multiple MIDI input devices. |
| selectOutput	| Select a MIDI output device. |
| selectOutputM	| Select multiple MIDI output devices. |
