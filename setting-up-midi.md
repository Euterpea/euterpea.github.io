# Setting up MIDI for Euterpea


[Back to Euterpea Home Page](https://euterpea.github.io/)

For Euterpea’s ``play`` functions and HSoM’s MUIs to work, you must have MIDI appropriately configured on your computer. 
The details of that configuration varies by operating system, but they share one major requirement in common: 
you must have a synthesizer installed and running to which Euterpea can send MIDI information. Sometimes this setup requires 
a virtual MIDI port, which is a software-level solution for letting two programs communicate via MIDI.

Euterpea’s ``play`` function sends output to your systems default MIDI device. If you are unsure what MIDI devices are 
present on your system or if you hear no sound using play, use the ``devices`` function to list available input and output devices. 
Sometimes the default MIDI device doesn’t work very well (or at all) and it can be better to use ``playDev`` to send from Euterpea 
to a different MIDI device or to change the default device on your system (if possible – see OS-specific details section further down). 
For example, suppose the devices function shows that your desired output device is number 4; you can then play music value ``m`` to 
that device by typing ``playDev 4 m`` into GHCi.

Some synthesizers show up as output devices, although you may need to manually run the program first before starting up GHCi or a 
compiled Euterpea program for it to be recognized.  For synthesizers that show up as devices, you can look up their device number using 
the ``devices`` function and then use ``playDev``. These devices will also show up in the output device list for HSoM’s MUIs using widgets like ``selectOutput``.

Other synthesizers won’t show up as a device at all – these require a virtual MIDI port to communicate between programs. On Windows, 
this involves installing extra software. On Mac and Linux, you can create virtual MIDI ports within the system settings. Once you have installed or 
created a virtual MIDI port, you must set the synthesizer to take input from the port and then send MIDI messages from Euterpea to the same port 
using ``playDev`` or, from within a MUI, ``selectOutput``. MIDI messages need to follow this path:

Euterpea --> Virtual MIDI Port --> Synthesizer


# MIDI Setup by Operating System

## Windows

For Windows XP through 8.1, there is no special setup required. The default MIDI output device will be the Microsoft GS Wavetable synth, which is not a great synthesizer but it works for basic purposes.
For Windows 10, usually there is no additional setup required, but occasionally machines that have been upgraded from earlier versions need a synthesizer installed.
See the MIDI on Windows page for more information.

## Mac

You will need to install a synthesizer like SimpleSynth or VMPK if you don’t already have one installed. Make sure the synthesizer 
running before you start GHCi or run a compiled Euterpea program. If using SimpleSynth, you may need to change the input port it is 
listening to (see additional setup info below).

Please note that the two most recent versions of OS X as of Jan 2014 have compatibility issues with SimpleSynth. To just verify that 
MIDI I/O with Euterpea is working, VMPK is a great alternative since it requires minimal setup. Before starting GHCi, just make sure 
VMPK is running, go into the options and enable omni and select CoreMidi (the default may be Network which won’t work). Then start up 
GHCi and try to play some notes.

See the MIDI on Mac (OX X) page for more information.


## Linux

See the MIDI on Linux page for a simple setup using Timidity as a synthesizer for Euterpea.

Euterpea requires [ALSA](http://www.alsa-project.org/main/index.php/Main_Page), which you may need to install.
You may also need to install alsa-seq by running: ``cabal install alsa-seq``.

# Additional helpful guides:

- [Ted’s Linux MIDI Guide](http://tedfelix.com/linux/linux-midi.html)

- [How to Use MIDI Sequecers with Soft Synths on Linux](http://tldp.org/HOWTO/MIDI-HOWTO-10.html)
  
- [Improving Your Linux System for Creating Music](http://www.rosegardenmusic.com/tutorials/qsynth-rosegarden/)

# Other Useful Programs

- [Virtual MIDI Piano Keyboard (VMPK)](http://vmpk.sourceforge.net/) is a cross-platform tool that can act as a synthesizer (taking MIDI input) and as a virtual keyboard (sending MIDI output). It requires a virtual MIDI port to communicate with Euterpea.

- [Sforzando](https://www.plogue.com/products/sforzando/) is a cross-platform synthesizer that supports the sf2 virtual instrument format.

- [FluidSynth](http://www.fluidsynth.org/) is a cross-platform synthesizer that supports the sf2 virtual instrument format.

- [Polyphony](http://polyphone-soundfonts.com/en/) is a cross-platform sf2 editor that can also serve as a synthesizer.

# Troubleshooting

I hear no sound from Euterpea’s play function.

If you are using a complicated Music value, first test something simple like ``play $ c 4 qn``. Check that audio is working on your computer (that sound isn’t muted, etc.). 
Try using the devices function to see what MIDI output devices are listed. You may need to use playDev instead of play. If devices returns no output devices, then you do not have a synthesizer running.

The output device or synthesizer I want isn’t listed by the devices function or by a MUI widget like selectOutput.

Make sure that hardware devices are connected and software synthesizers are running before starting GHCi or running a Euterpea program that has been compiled with GHC.
If you just installed the software for a device/synth, you may also need to reboot before it is recognized.
