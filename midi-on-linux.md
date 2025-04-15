**Please note: the information on this page is rather extremely old and has not been updated in a long time. Some parts may need updating.**

# MIDI on Linux

[Back to Euterpea Home Page](https://euterpea.github.io/)

Last modified: Jan 18, 2019 @ 1:26 pm

The easiest way to get MIDI output from Euterpea with Linux is to use Timidity. You can also use FluidSynth or any other Linux-compatible MIDI synthesizer, 
but Timidity is typically the simplest to get up and running for the first time. Regardless of which synthesizer you use, you will need to start it BEFORE you load Euterpea.

The installation commands here are shown using the apt package manager. If you are using a different package manager (like yum), you will need to check the availability of the packages and modify the commands accordingly.

Note: you must have ALSA installed to use Euterpea and/or Timidity. You can do this with:
sudo apt-get install libasound2-dev

Using Timidity with ALSA is describd in the next section. If you want to use FluidSynth instead, follow the instructions HERE for configuring it as an ALSA daemon.

## Using Timidity as a Synthesizer
On Ubuntu/Debian/etc. you can do it this way:

Open a terminal.

Install Timidity by running: ``sudo apt-get install timidity``

Start the timidity daemon with: ``timidity -iA -Os``
(When you want to close it after you’re done, use Ctrl+C)
- Leave that terminal window open in the background and open a NEW terminal window.

Run:
```
ghci
import Euterpea
devices
```
You should see something like this:
```
Input devices:
InputDeviceID 1  Midi Through Port-0
Output devices:
OutputDeviceID 0 Midi Through Port-0
OutputDeviceID 2 TiMidity port 0
OutputDeviceID 3 TiMidity port 1
OutputDeviceID 4 TiMidity port 2
OutputDeviceID 5 TiMidity port 3
```

You want to use the first thing called “TiMidity port” – NOT the Midi Through Port. If you accidentally play to the Midi Through, 
you will hear no sound. In this case, the first actual TiMidity port is device number 2, so subsequent examples will use that port number. 
Because Euterpea’s play function uses device 0 by default, you need to use the playDev function instead and specify the device number like this:

``playDev 2 $ c 4 qn``
