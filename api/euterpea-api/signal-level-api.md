# Signal-Level API

**Please note:** all of the functions described here are for *offline* sound synthesis only! 
If you want to define virtual instruments that interact with Euterpea in real time, take a look at the [VividEuterpea](https://github.com/donya/VividEuterpea) repository, 
which provides a bridge between Euterpea’s music structures and constructing instruments using the Vivid library for real time audio in Haskell.

This page gives a list of important datatypes and functions in Euterpea for working with music at the signal level. 
For more information on the functions, types, and type classes listed here, please see the Haskell School of Music textbook or, 
from GHCi with Euterpea imported, type the following:

``:i nameYouWantToKnowAbout``

## Instrument Creation and Usage

| Function/Type	| Description |
| ----- | ----- |
| Instr | a	Polymorphic instrument definition. |
| InstrMap | a	Table to link an InstrumentName with an Instr |
| InstrumentName	| Type synonym for String |
| outFile	| Write a finite amount of a signal function to a WAV file. |
| renderSF	| Convert a Music value using custom instruments to a signal function. |
| writeWav	| Convert a Music value using custom instruments to a WAV file (combines renderSF and outFile). |

## Signal Functions

| Function/Type	| Description |
| ----- | ----- |
| Table	| For representing a series of audio samples with/without normalization. |
| balance	| Adjusts RMS amplitude to match a reference amplitude. |
| delayLine	| Delay a signal by a fixed amount of time. |
| delayLine1	| Delay line with 1 tap. |
| delayLineT	| Delay line for a Table. |
| envASR	| Attack-sustain-release envelope. |
| envCSEnvlpx	| Slightly different ASR envelope interface. |
| envExpon	| Exponential envelope |
| envExponSeg	| Envelope of exponential segments. |
| envLine	| Linear envelope |
| envLineSeg	| Envelope of linear segments. |
| filterBandPass	| Band-pass filter. |
| filterBandPassBW	| Butterwoth band-pass filter. |
| filterBandStop	| Band-stop filter. |
| filterBandStopBW	| Butterworth band-stop filter. |
| filterComb	| Comb filter. |
| filterHighPass	| High-pass filter. |
| filterHighPassBW	| Butterworth high-pass filter. |
| filterLowPass	| Low-pass filter. |
| filterLowPassBW	| Butterworth low-pass filter. |
| noiseBLH	| Band-limited noise generator without interpolation. |
| noiseWhite	| White noise generator. |
| nosieBLI	| Band-limited noise generator with interpolation. |
| osc	| Oscillator for a Table |
| oscDur	| Delated oscillator that stays at the first sample for a set amount of time. |
| oscDurI	| Like oscDur, but with linear interpolation |
| oscFixed	| A simple, fast sine oscillator. |
| oscI	| Like osc but uses linear interpolation. |
| oscPartials	| Oscillator for harmonically-related sinewave partials. |
| pluck	Pluck | filter for a Table of samples. |
| tableBesselN / tableBessel	| Generates the log of a modified Bessel function. For use with AM/FM modulation with/without normalization. |
| tableExponN / tableExpon	| Create a Table from coordinates using expontential interpolation with/without normalization. |
| tableLinearN / tableLinear	| Create a Table from coordinates using linear interpolation with/without normalization. |
| tableSines3N / tableSines3	| Create a Table from sinewave partials given their partial number, strength, and phase offset with/without normalization. |
| tableSinesN / tableSines	| Create a Table from sinewaves with the specified partial strengths with/without normalization. |

## Miscellaneous Functions

| Function	| Description |
| ------ | ----- |
| apToHz	| Convert an AbsPitch (or pitch number) to Hertz. |
| pchToHz	| Convert a Pitch value to Hertz. |
