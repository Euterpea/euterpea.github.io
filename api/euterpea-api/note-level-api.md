# Euterpea Note-Level API

This page gives a list of important datatypes and functions in Euterpea for working with music at the “note level,” or roughly at the level of a paper score. 
For more information on the functions, types, and type classes listed here, please see the Haskell School of Music textbook or, from GHCi with Euterpea imported, type the following:

``:i nameYouWantToKnowAbout``

## Music Types and Type Classes

| Type/Class	| Description |
| ---------- | ------------- |
| AbsPitch	| Type synonym for Int. |
| Control	| For use with Music's Modify constructor. |
| InstrumentName	| For GM instruments. |
| MEvent	| Event representation for notes. Used in conversion from Music to MIDI. |
| Mode	| Tonality. Currently only Major and Minor are supported. |
| Music a	| Polymorphic structure for representing music. |
| Music1	| Type synonym for Music1 or Music (Pitch, \[NoteAttribute]). |
| Note1	| Type Synonym for (Pitch, [NoteAttribute]). |
| NoteAttribute	| For use with Music1. |
| Octave	| ype synonym for Int. |
| Performance	| Type synonym for \[MEvent] |
| PhraseAttribute	| For use with Control. |
| Pitch	| Type synonym for (PitchClass, Octave) |
| PitchClass	| Representation of pitch classes. |
| Primitive	| A Note or a Rest. |
| ToMusic1	| Type class with one function, toMusic1, for converting to Music1. Instances are included for Pitch, (Pitch, Volume), AbsPitch, (AbsPitch, Volume), and Note1. The ToMusic1 type class is required for the play function. |

## Playback Functions and Types

| Function	| Description |
| ---------- | ------------- |
| devices	| Print a list of available MIDI devices and their corresponding device numbers. |
| play	| Play a Music value to the default MIDI output device. Supports infinitely long Music values. |
| playC	| Custom playback using the PlayParams data structure. |
| playDev	| Play a Music value to a custom MIDI output device. Supports infinitely long Music values. |
| playDevS	| Play a finite Music value to a custom MIDI output device with strict timing. |
| PlayParams	| Record type to control playback behavior with playC. |
| playS	| Play a finite Music value to the default MIDI output device with strict timing. |

**Note:** the play function is lazy and does *not* guarantee millisecond-correct timing! For more information on the implementation of play and playS, please see this post on the subject.

## Music Manipulation

| Function	| Description |
| ---------- | ------------- |
| changeInstrument	| Changes the instrument of a Music value and Removes any nested Instrument modifiers. |
| chord	| Put a list of music values together in parallel. |
| chord1	| Like chord but requires a non-empty list and does not add any zero-length rests. |
| cut	| Take a finite portion of Music from the front of the value. |
| forever	| Repeat a Music value infinitely. |
| instrument	| Adds an Instrument modifier. |
| invert	| Inverts (flips upside down) a Music Pitch value around its first pitch. |
| invert1	| Like invert but for Music (Pitch, a). |
| invertAt	| Inverts a Music Pitch value around a specified Pitch. |
| invertAt1	| Like invertAt but for Music (Pitch, a). |
| invertRetro	| Performs retrograde then inversion. |
| keysig	| Adds a KeySig modifier. |
| line	| Put a list of music values together sequentially. |
| line1	| Like line but requires a non-empty list and does not add any zero-length rests. |
| lineToList	| Opposite of line. |
| mFold	| Like fold but over Music values. |
| mMap	| Like map but over Music values. Operates over all "a" portions of a "Music a" |
| note	| Creates a single Note. |
| offset	| Delay a the onset of a Music value. |
| perc	| Creates a note wrapped with the Percussion instrument. |
| phrase	| Adds a Phrase modifier. |
| remove	| Remove a finite portion from the front of a Music value. |
| removeInstruments	| Strips all Instrument modifiers from a Music value. |
| removeZeros	| Strip zero-duration constructs from a Music value. |
| rest	| Creates a single Rest. |
| retro	| Reverses a Music value. |
| retroInvert	| Performs inversion then retrograde. |
| scaleDurations	| Alters the durations of a Music value. |
| shiftPitches	| Shifts all pitches in a Music Pitch value by the specified amount. |
| shiftPitches1	| Shifts all pitches in a Music(Pitch,x) value by the specified amount. |
| tempo	| Adds a Tempo modifier. |
| times	| Repeat a Music value sequentially for a fixed number of times. |
| transpose	| Adds a Transpose modifier. |

## MIDI Conversion Functions

| Function	| Description |
| ---------- | ------------- |
| exportMidiFile	| Writes a Midi value to a file. |
| fromMidi	| Converts a Midi value to a Music1 value. |
| importFile	| Reads a MIDI file to a Midi value. |
| perform	| Converts a Music value to a Performance. Requires an instance of ToMusic1. |
| toMidi	| Converts a Performance to a Midi value. |
| writeMidi	| Writes a Music value to a MIDI file. Requites a ToMusic1 instance. |

# Extra MIDI-Related Functions

| Function Name	| Module	| Description |
| ----- | ----- | ------ |
| restructure	| Euterpea.IO.MIDI.FromMidi2	| Attempts to group musical features by obvious chords, melodies, and so on. The restructure function can be used on Music values that have been read in from MIDI files (the default representation for which is all notes combined in parallel with rests). |
| writeMidi2	| Euterpea.IO.MIDI.ToMidi2	| Allows exporting of MIDI files where more than one track can have the same instrument. To use this, all Instrument assignments must be done using CustomInstrument with a String of the format "GMName UniqueID" (for example: "Flute A") |

