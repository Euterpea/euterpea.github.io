**Please note: the information on this page is rather extremely old and has not been updated in a long time. Some of it is still relevant, some not.**

Last modified: Nov 2, 2017 @ 8:22 am

This page is intended specifically for Euterpea 2 users. If you are not a Euterpea user or are using the older Euterpea 1.1.1, you may find one of these other pages more helpful:

MIDI on Windows for Euterpea 1.1.1
MIDI on Windows outside of a DAW (for non-Euterpea users)
Introduction
Working with MIDI on Windows can be a tricky thing when one wants to go beyond simply playing MIDI files and using the play and writeMidi functions in Euterpea. Four topics are covered here:

Getting MIDI Output
Getting MIDI Input
Minimizing Playback Latency
Setting the Default MIDI Output Device.
Playback on Windows 10
 


Getting MIDI Output
Usually Windows comes with a default MIDI synthesizer that will show up as the default MIDI output device. However, if you are unable to use Euterpea’s play function due to lack of a MIDI output device (which is rare, but nevertheless possible), you can use the solutions later on this page for minimizing playback latency via another synthesizer or you can use this version of JavaOx, a small program that routs MIDI messages and allows the user to send to Java’s on synthesizer. To run JavaOx, you will need a Java Runtime Environment. You will also need a virtual MIDI port such as LoopBe1. You can then use the devices function to see what the numbers are for your installed MIDI devices and then use playDev to play to a specific device.

where x is the device ID number as shown by the devices function – run it in GHCi to list all available MIDI devices and their numbers. You can then set JavaOx to take input from the virtual MIDI port and send it to Gervill, which is Java’s synthesizer. Note that this approach is simple, but it will not give you low latency. In fact, the latency will be about as bad as when using the the Microsoft synthesizer that is typically bundled with Windows. If you need low latency solutions, skip to the section on Minimizing Playback Latency.

For the best possible timing during playback of finite Music values, you may also wish to use the playS function (S being short for “strict”). For playback to a specific device, there is also playDevS. However, be aware that both of these will hang on infinite values, since the Music value is evaluated fully before attempting playback.

 


Getting MIDI Input
Windows comes with a MIDI synthesizer, the Microsoft GS Wavetable Synth. This synthesizer allows the playback of MIDI files and will play any MIDI events streamed to it in real-time (albeit with horrible lag, which will be addressed later). However, there is no way to take input from this synthesizer, and there are no other MIDI input devices by default. Many modern MIDI hardware devices that connect by USB, such as small keyboards, will show up as a MIDI input device once installed. However, there are also software alternatives that allow for MIDI input from a virtual keyboard. One software-only solution is to do the following:

Install a virtual MIDI port like LoopBe1 (1 port) or LoopMIDI (multiple ports possible). Let’s call this virtual port Port1.
Install a virtual MIDI keyboard like Proxima Controller.
To be totally safe and minimize troubleshooting, reboot before you try any MIDI I/O, even if it looks like it should work.
Set the virtual keyboard (Proxima Controller) to send output to Port1.
In your primary program of interest, such as a Euterpea MUI, you can now take input from Port1 and send output to the MS Wavetable Synth.
This will allow basic MIDI I/O. However, you will hear a noticeable delay between pressing a key in a program like Proxima Controller (or on a hardware keyboard for that matter) and hearing any output, even if sending events directly to the MS Wavetable Synth rather than through a virtual MIDI port first.

You only need one virtual port for taking input. LoopBe1 givese you a single port that is very easy to use and automatically runs in the background when Windows starts; it is the easiest solution for anything requiring only one port. LoopMIDI allows more ports, which can be necessary for achieving low-latency MIDI I/O as described later on, but you have to set up the ports manually and specify whether you want it to auto-start. Note: when using a virtual MIDI port, make sure that you don’t set the port to send and receive from itself. With LoopBe1, you will get a feedback error and the program will mute itself (which has to be fixed via the icon in the system tray).


Minimizing Playback Latency
The MS Wavetable synth often exhibits a delay of 100ms or more between the time an event is sent and when any sound starts. The delay is quite noticeable on most machines. Unfortunately, there is no way to fix the latency with that synth. The only way to lower MIDI I/O latency without a hardware synthesizer is to get a different software synth that gives you some control over the setting directly and/or control over the audio drivers it uses – which must be low-latency drivers. Getting a different synth is pretty easy, since there are some good freeware/shareware programs for it. Two such programs are CoolSoft’s VirtualMIDISynth, and SyFonOne. A third commonly used option is Sforzando. If you are working purely with your on-boar sound chip (integrated sound) rather than an external audio interface with special drivers, the CoolSoft synth will likely yield the best performance.

All of those programs make use of a virtual instrument format called SoundFonts, or sf2, which was developed by Creative Labs. An sf2 file is a collection of instruments mapped to different patch numbers. Because sf2 files can be quite large, they are often stored in the compressed sfark format. SyFonOne comes with a sample sf2 file, but the Coolsoft synth does not. You can get some sf2 files from HERE. Some older PCI/PCIe sound cards have built-in support for sf2 and can provide low-latency playback without the use of additional software synthesizers (the current list of compatible devices is at the bottom of this page).

CoolSoft’s VirtualMIDISynth allows you to have some control over the output latency without needing special drivers. To minimize the latency, go into Configuration > Options > Advanced Options and set the additional output buffer lower. I usually recommend starting with a value of 10 and testing playback with at least some chords in it to hear some MIDI polyphony. Some systems can go as low as 0 latency with this synth, although this is somewhat rare and requires a pretty beefy machine (often a desktop tower and good audio hardware). Many lesser machines, however, will still work with 5-7ms. Depending on the particular machine and its settings higher latencies may be required to avoid distortion, clicks, and/or audio dropouts. On laptops in particular, the degree to which you can reel in the latency can be affected by power settings. High performance modes can typically function with lower latencies without audio glitching than battery saving modes are capable of.

The driver control situation is more complicated, since some programs require ASIO drivers for good performance (ASIO = Audio Stream I/O, a particular protocol), and on-board sound almost never comes with that type of driver. Most high-end audio interfaces have ASIO or other low-latency drivers. For example, the M-Audio FastTrack series and the Tascam US series audio interfaces come with their own ASIO drivers.

There is also a nice program called ASIO4All that will work with the synths described so far and any audio device with WDM drivers (present on most Windows machines). This program gives very good performance even with on-board sound in the absence of an expensive audio rig. However, it has one significant limitation: it requires exclusive use of an audio device. So, for example, you can’t use ASIO4All with a software synth at the same time as playing something in Windows Media Player if you only have one audio device. Still, ASIO4All is one of the easiest options for achieving better playback latency without extra hardware, and it is only problematic in special cases where a device has to be shared between several programs simultaneously. This limitation is not unique to ASIO4All, and some low-latency audio interfaces are also single-client. The ASIO Multiclient Wrapper is one option to achieve multi-client playback in these situations.

Here is an example setup using ASIO4All:

Install a virtual MIDI port as described in the previous section. We’ll call it Port2.
Install ASIO4All.
Install SyFonOne and reboot.
Open SyFonOne, tick the ASIO box under the options window (sometimes it’s a good idea to actually close SyFonOne after this change and open it again), take input from Port2 and hit “play.”
Send MIDI events to Port2 to hear playback. In a Euterpea MUI, Port2 should be the output device.
You may need to fiddle with the settings in ASIO4All for a few minutes if it fails to have the correct things enabled and disabled the first time it runs. The devices usually have ambiguous names like “HD Output 1,” so it can be hard to know what should be on/off on some systems when there are multiple devices listed.

NOTE: see how Port2 already has something sending to it and receiving from it in the setup above? This means that you can’t use it to do MIDI input as well from other software like Proxima Controller. If you need to do MIDI input from such a program and have low latency with the method described above, then you need to use a multi-port option like LoopMIDI, since LoopBe1 will not let you do all of those things simultaneously.

Another solution for this issue if you have a hardware MIDI interface with its own ASIO drivers is to have one virtual MIDI port (like LoopBe1) and one MIDI cable that sends from the hardware interface back into itself. The hardware interface should show up as an input and output device, so you can send from ProximaController to a MUI with a virtual port and then send from the MUI to a synth with the hardware interface (or similarly with the virtual and hardware ports reversed). Connecting a device to itself may seem like an ugly hack, but the performance can actually be really good.

So, what about hardware that has low-latency drivers that aren’t ASIO? Some systems have WDM or MME drivers that really can perform well. If you know that your hardware should be capable of good performance with the drivers it has, then you can use JACK to trick programs like the soft-synths described above into using your non-ASIO drivers anyway. JACK wraps your existing drivers and presents an ASIO interface to other software. If you want to do this, you can set up JACK as follows:

Install JACK and reboot. Then, open the Jack Control executable.
Under the Setup window’s options, you want the server prefix to be “jackd -S”, the driver to be “portaudio”, and the interface to be your driver of choice. Save the settings and close the setup window but don’t close the main window.
Start the audio server with the “Start” button. You will need to keep this running while you use your soft-synth. Your synth may crash if JACK is closed before the synth is. If JACK crashes or gives an error when you try to start the server, check that there are no other programs trying to use the same audio device.
Open your soft-synth and you should now see JACK (by the name JackRouter) as an ASIO option.

Setting the Default MIDI Output Device
Windows XP: easy! Go into the recording and playback devices and select the option you want.

Windows Vista and 7: the XP option no longer exists, but the functionality does. There are several tools out there for doing this, such as PLW MIDI Mapper and Vista MIDI. Both actually work on Windows 7 as well as Vista despite their names, but you may need to run the programs as an administrator and/or reboot before the changes will take effect.

Windows 8, 8.1, and 10: for these versions, there is no way of manually setting the default synthesizer within Windows itself. Note: this does NOT mean that you cannot set a different synthesizer within other software packages. Most music software lets you do this unless it is quite old (such as pre-WinXP). If you have software like Sibelius, Finale, Cakewalk, Cubase, etc., you can definitely set the default output but you have do it within the program rather than via Windows settings. Euterpea also has support for device-specific playback using the playDev function (along with devices to list available MIDI outputs), and HSoM’s MUIs support sending to user-specified devices via widgets like selectOutput. More recently, CoolSoft also released the CoolSoft MIDI Mapper, which re-adds the MIDI mapper functionality for more recent versions of Windows. My testing of that program has been extremely limited, but it has worked so far for me on one machine running the Windows 10 fall creator’s update. To get the CoolSoft MIDI Mapper, you will need to register on the site to gain access to the download links in this thread, as it currently isn’t available for download elsewhere.


Playback on Windows 10
The play function should work on most recent builds of Windows 10. However, right after the operating system’s initial release, there were known problems with the default synth on Windows 10 that caused backwards compatibility problems with some older MIDI software, including Euterpea, wher trying to use play after upgrading from an older Windows version to Windows 10 resulted in host errors from the default MIDI output device. The problem went away on some machines with later Windows updates and clean installations of Windows 10 appear to be working just fine as of December 2015.

If play gives you host errors on Windows 10, the easiest solution (other than a completely clean install of the OS) is to install Coolsoft’s VirtualMIDISynth. The Coolsoft synth should become the default output device (for more than just Euterpea) and play should work again. This behavior is actually quite strange, because the answer given repeatedly from Microsoft for Windows 8 and later versions is that there is no way to perform this type of alteration even with invasive manual registry editing. Of course, if play was already working for you with the default synth on Windows 10, installing the Coolsoft synth will have no effect on the default output device.

Alternatively, if you have another synthesizer and/or a virtual MIDI port installed that you would like to use, you can use the devices function to look up relevant MIDI device numbers and then use playDev to send output to a custom device. If installed, the Coolsoft synth will show up as an option with playDev as well as with HSoM’s selectOutput widget for MUIs. The Coolsoft synth is configurable to have much lower latency than the default Windows synth, making it a useful tool even aside from strange bug fixes.
