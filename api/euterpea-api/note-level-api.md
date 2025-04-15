# Euterpea Note-Level API

This page gives a list of important datatypes and functions in Euterpea for working with music at the “note level,” or roughly at the level of a paper score. 
For more information on the functions, types, and type classes listed here, please see the Haskell School of Music textbook or, from GHCi with Euterpea imported, type the following:

``:i nameYouWantToKnowAbout``

## Music Types and Type Classes

Type/Class	Description
Primitive	A Note or a Rest.
Music a	Polymorphic structure for representing music.
Note1	Type Synonym for (Pitch, [NoteAttribute]).
Music1	Type synonym for Music1 or Music (Pitch, [NoteAttribute]).
ToMusic1	Type class with one function, toMusic1, for converting to Music1. Instances are included for Pitch, (Pitch, Volume), AbsPitch, (AbsPitch, Volume), and Note1. The ToMusic1 type class is required for the play function.
PitchClass	Representation of pitch classes.
Octave	Type synonym for Int.
Pitch	Type synonym for (PitchClass, Octave)
AbsPitch	Type synonym for Int.
Control	For use with Music's Modify constructor.
Mode	Tonality. Currently only Major and Minor are supported.
InstrumentName	For GM instruments.
PhraseAttribute	For use with Control.
NoteAttribute	For use with Music1.
MEvent	Event representation for notes. Used in conversion from Music to MIDI.
Performance	Type synonym for [MEvent]

## Playback Functions and Types

Function	Description
play	Play a Music value to the default MIDI output device. Supports infinitely long Music values.
playDev	Play a Music value to a custom MIDI output device. Supports infinitely long Music values.
playS	Play a finite Music value to the default MIDI output device with strict timing.
playDevS	Play a finite Music value to a custom MIDI output device with strict timing.
playC	Custom playback using the PlayParams data structure.
devices	Print a list of available MIDI devices and their corresponding device numbers.
PlayParams	Record type to control playback behavior with playC.
Note: the play function is lazy and does not guarantee correct timing. For more information on the implementation of play and playS, please see this post on the subject.

## Music Manipulation

Function	Description
note	Creates a single Note.
rest	Creates a single Rest.
line	Put a list of music values together sequentially.
line1	Like line but requires a non-empty list and does not add any zero-length rests.
chord	Put a list of music values together in parallel.
chord1	Like chord but requires a non-empty list and does not add any zero-length rests.
lineToList	Opposite of line.
invert	Inverts (flips upside down) a Music Pitch value around its first pitch.
invert1	Like invert but for Music (Pitch, a).
invertAt	Inverts a Music Pitch value around a specified Pitch.
invertAt1	Like invertAt but for Music (Pitch, a).
retro	Reverses a Music value.
invertRetro	Performs retrograde then inversion.
retroInvert	Performs inversion then retrograde.
offset	Delay a the onset of a Music value.
times	Repeat a Music value sequentially for a fixed number of times.
forever	Repeat a Music value infinitely.
cut	Take a finite portion of Music from the front of the value.
remove	Remove a finite portion from the front of a Music value.
removeZeros	Strip zero-duration constructs from a Music value.
mMap	Like map but over Music values. Operates over all "a" portions of a "Music a"
mFold	Like fold but over Music values.
transpose	Adds a Transpose modifier.
tempo	Adds a Tempo modifier.
instrument	Adds an Instrument modifier.
phrase	Adds a Phrase modifier.
keysig	Adds a KeySig modifier.
shiftPitches	Shifts all pitches in a Music Pitch value by the specified amount.
shiftPitches1	Shifts all pitches in a Music(Pitch,x) value by the specified amount.
scaleDurations	Alters the durations of a Music value.
changeInstrument	Changes the instrument of a Music value and Removes any nested Instrument modifiers.
removeInstruments	Strips all Instrument modifiers from a Music value.
perc	Creates a note wrapped with the Percussion instrument.

## MIDI Conversion Functions

Function	Description
perform	Converts a Music value to a Performance. Requires an instance of ToMusic1.
toMidi	Converts a Performance to a Midi value.
exportMidiFile	Writes a Midi value to a file.
writeMidi	Writes a Music value to a MIDI file. Requites a ToMusic1 instance.
importFile	Reads a MIDI file to a Midi value.
fromMidi	Converts a Midi value to a Music1 value.
Extra MIDI-Related Functions
Function Name	Module	Description
restructure	Euterpea.IO.MIDI.FromMidi2	Attempts to group musical features by obvious chords, melodies, and so on. The restructure function can be used on Music values that have been read in from MIDI files (the default representation for which is all notes combined in parallel with rests).
writeMidi2	Euterpea.IO.MIDI.ToMidi2	Allows exporting of MIDI files where more than one track can have the same instrument. To use this, all Instrument assignments must be done using CustomInstrument with a String of the format "GMName UniqueID" (for example: "Flute A")
