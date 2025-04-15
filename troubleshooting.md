# Troubleshooting


[Back to Euterpea Home Page](https://euterpea.github.io/)


Information last updated: Jan 10, 2024

This page has Euterpea and HSoM general problems listed first followed by OS-specific issues. 
If you have a specific error message, you may also be able to find it quickly by searching the page for a 
small portion of the error message (for example, if you have an error that involves the term PMMsg, try searching for that word on the page).

Please keep in mind if you have a very old (10+ years) or very new (just released) Mac/Windows operating system version, 
it may be beyond the currently supported spec. Linux distributions are also very hit and miss – Ubuntu usually succeeds, 
but more niche distributions like Nix OS are likely to have issues.

Check the "general problems" section first if you have installation issues or problems with the ``play`` function. 
If you don’t see your problem there, check under your operating system’s category.

If you did not find your problem listed on this page, please report the details of your operating system, which versions 
of GHC and cabal you are using (``ghc --version`` and ``cabal --version``), what led to the problems, and the error messages that were produced on the issues page for 
Euterpea 2 or the issues page for HSoM depending on which library caused the problem. Installation problems should include a 
*complete transcript* of what you ran showing the failed installation all the way from ``cabal install`` onward. 
Please do NOT use pull requests to report bugs or suggest fixes.


# General Problems (Installation & Play)

## Installation

**Installing Euterpea on Linux with v1-style commands appears to succeed but GHCi can’t find Euterpea (“Could not find module ‘Euterpea'”)** \
Euterpea is not guaranteed to succeed on all types of Linux. Most successful installations use older versions of GHC. If you have a newer GHC version, you can try using the “–lib” flag:\
``cabal install --lib --allow-newer``\
However, while this may allow Euterpea to be imported into GHCi for basic usage, you may not be able to install any other libraries that depend on Euterpea (and it will not be visible when doing “ghc-pkg list”).

**Running “cabal update” then “cabal install” fails errors related to Heap or old Euterpea versions (pre-2.0).** \
This can happen if cabal fails to obtain the updated package list from Hackage. You may need to run ``cabal v1-update`` to successfully pull the most recent set of packages from Hackage. 
If the update is successful, you will see a message instructing you how to revert to a previous version.

**The “cabal install” step appeared to succeed, but the Euterpea package can’t be found with “import Euterpea.”** \
If you are running any extra antivirus software beyond what your OS comes with, try temporarily disabling it and running the installation again. 
Some antivirus programs may silently block actions required for a successful 
installation when running the cabal install – even in administrator mode on Windows. In some cases the installation may appear to succeed when 
it is actually incomplete. 

**A call to "caball install” fails unexpectedly partway through the installation with no error beyond “some packages failed to install” when installing either Euterpea or a new version of cabal.** \
If the installation requires downloading additional packages, a timeout during the download can cause the installation to abort unexpectedly. 
Unfortunately this can be a persistent problem on slow or unstable connections such as those by satellite or when tethering to a mobile device with poor signal. 
Check your Internet connection, verify that hackage.haskell.org is up and running, and try again. Sometimes the hackage website experiences problems/downtime, 
in which case you may need to wait a while to install Euterpea with cabal.

**The installation fails with errors relating to PMMsg.** \
You have tried to install an out-dated version of Euterpea. If you were trying to install from Hackage, please run “cabal update” and try again. 
If you are using a manual download, make sure you have the most recent version from either Hackage or GitHub.

**After installing Haskell Platform, “cabal” is an unrecognized command.** \
Either your PATH variable wasn’t updated (an issue for old Haskell Platform versions) or something blocked it being updated (an issue with administrative privileges or antivirus software).
You can fix this manually: locate your cabal\bin (Windows) or cabal/bin (Linux and Mac) folder and add it to your system’s PATH environment variable. 
The PATH is a collection of folder names that your computer checks when looking for programs invoked by commands. Steps for editing the PATH differ by operating system; 
look up the procedure that is appropriate for your computer and OS version. Note that the procedure on more recent builds of Windows 10 is different from previous versions of Windows. 
For Mac and Linux users, make sure you permanently edit the path (typically requires editing a file), otherwise cabal will fall out of scope again the next time you open a terminal.

**After installing Haskell Platform, cabal is in scope but ghc/ghci are not.** \
The executables for GHC and GHCi may have been installed to another location (an issue with some old OS and Haskell Platform versions). 
Search for the ghc and ghci executables on your computer and manually add the appropriate folders to your PATH as in the troubleshooting item above.

**Installing Euterpea and/or HSoM fails with errors related to HCodecs.** \
Euterpea briefly experienced problems with platform version 8.4.2, but changes were pushed to both Hackage and GitHub to correct the issue. 
To get these changes, you need to run cabal update before running cabal install Euterpea (newer GHC version users will need to use the v1-style commands, v1-update and v1-install with the –allow-newer flag)

## Playback

**Using play or playDev drops notes sometimes.** \
The ``play`` and ``playDev`` functions are lazy. Try using playS or playDevS with a finite portion of your music value and seeing if the problem persists – 
if it does then the problem likely is with your music value and/or synthesizer (check for durations <=0 and overlapping notes with the same pitch and instrument). 
However, if playS/playDevS perform the music correctly while play/playDev do not, it is likely an issue with simultaneous MIDI messages arriving in the wrong order to your MIDI device. 
If you are using Euterpea 2.0.7 or earlier, consider installing Euterpea 2.0.8 from GitHub, which has a fix for this situation.

**The “play” function produces no sound from within GHCi.** \
Check that your sound device is enabled and that the volume is set correctly. On Mac and Linux, you need to have a synthesizer running before GHCi is started. 
Follow the instructions for Setting up MIDI, restart GHCi, and then try again. Windows users: play is not guaranteed to work with GHCi on 64-bit versions of Haskell Platform.

**The “play” function gives a “No MIDI output device found” error.** \
This means there are no active MIDI output devices on your system. Use the “devices” function in GHCi to list available output devices. 
On Mac and Linux, you need to have a synthesizer running before GHCi is started. Follow the instructions for Setting up MIDI, restart GHCi, and then try again.

**When playing a Music value, Euterpea plays some instruments, but others are silent despite appearing in MIDI file output with velocities >0.** \
This is likely an issue with your synthesizer, not Euterpea. Some synthesizers do not have patches for all of the general MIDI instruments.
Try using a different synthesizer or a different set of virtual instruments. It may also be an issue with what channel MIDI messages are being sent to if you are using a custom channel assignment function.


# Windows-Specific Problems
**Euterpea’s play function causes one or more instances of the following error message: addLibrarySearchPath: D:\GitHub\haskell-platform\build\ghc-bindist\local\mingw\lib (Win32 error 3): The system cannot find the path specified.** \
This is due to a problem with the compiled binaries in a now outdated release of Haskell Platform 8.4.3 and 8.4.2. 
Uninstall Haskell Platform, re-download Haskell Platform 8.4.3 to get the corrected binaries, and then re-install. 
There is a thread on the issue on Haskell Platform’s GitHub issues page: https://github.com/haskell/haskell-platform/issues/312

**Calling the “play” function on any Music value or trying to send MIDI messages to the default Windows synthesizer gives “host error” messages with no sound.** \
First, make sure your sound device is enabled, close all other applications, and restart GHCi. Some programs will “grab” audio and MIDI devices in an
exclusive way and will note release them for other applications to use (recent versions of Chrome are particularly bad for this!). 
On some Windows 10 installations, primarily those upgraded from older version of Windows, the default MIDI synthesizer may not work correctly; 
the easiest fix is to install the Coolsoft Virtual MIDI Synthesizer. Please see the Midi on Windows page for more information.

**Trying to start GHCi, WinGHCI, or running GHC fails with errors related to pthread.dll, such as: user specified .o/.so/.DLL could not be loaded (addDLL: pthread or dependencies not loaded. (Win32 error 193))** \
If you have Lilypond installed, this is unfortunately a known incompatibility with recent versions of Haskell Platform right now. There are only three ways to solve it for now:

- Option 1: Remove Lilypond’s bin folder from your PATH environment variable. If you have a user path and a system path,
you must remove Lilypond-related entries from BOTH, not just the user’s path. You may need to reboot for GHCi to work again.
You should still be able to run the GUI for Lilypond by making a desktop shortcuts directly to Lilypad.exe. If using from command line,
calling the executables with the full path to the containing folder. Unless you used a custom installation location,
the Lilypad, lilypond, midi2ly, and other programs that come with Lilypond will be located in this folder:
C:\Program Files (x86)\LilyPond\usr\bin

- Option 2: Use Haskell Platform 8.0.2a (core or full).

- Option 3: Uninstall Lilypond. This is only recommended if it’s an old installation and you don’t plan on using it anymore. Otherwise, try option 1 first.

If you are getting errors related to pthread.dll without ever having had a Lilypond installation, please report the problem on Euterpea2’s Issues page on GitHub.

**Calling the “play” function on any Music value crashes GHCi. ** \
This can happen with the 64-bit versions of Haskell Platform on pre-creators update Windows 10 and on any version of Windows with Haskell Platform 8.0.1 or earlier. For older versions of Windows and/or older versions of  Haskell Platform, please use the 32-bit version on Windows if you want to work within GHCi. Alternatively, try compiling your program to an executable with GHC.

**After installing Haskell Platform, “cabal user-config init” doesn’t work.** \
Try running “cabal update” first, which will also tell you where the config file is.

**Double-clicking to open hs/lhs files with GHCi crashes with an error.**\
When the creator’s update was initially released, it broke the double-click-to-open functionality for hs/lhs files and GHCi. 
This seems to have been resolved on most machines with some later incremental Windows updates later in 2017, so please run Windows 
Update to make sure your machine is up-to-date. If you still have problems, you should still be able to run ghc and ghci manually 
from a command prompt or Power Shell – if you can’t, then there is a problem with your Haskell Platform installation and you should 
uninstall and reinstall. Another workaround is to use WinGHCi as the default program for opening Haskell source files.

**The GHCi window immediately crashes/disappears when opening a Haskell source file (.hs/.lhs) by double-clicking it.** \
This is a known issue with GHCi and the initial realize of the Windows 10 Creators Update. Please run Windows Update, restart, and 
see if the problem persists. If it does, the best workarounds are to either run GHCi from within a command prompt (or PowerShell) 
and load the file manually or use WinGHCi as the default program to open source files.

**(Windows, HSoM) Trying to run one one of HSoM’s MUIs results in a GLUT-related error.**\
Some machines end up with out-dated versions of glut.dll, which is a file needed to run MUIs and other programs using the UISF library, 
and others may lack it altogether. Haskell Platform comes with an appropriate version of glut.dll, but it doesn’t always end up in the
system path. There are two options: (1) copy Haskell Platform’s glut.dll and replace older versions on your machine or 
(2) add the location of Haskell Platform’s glut.dll to your system’s path variable.


# Mac-Specific Problems

**Trying to install a GHC version between 8.2.2 and 9.4.6 gives a cryptic error about “sh”** \
Your xcode version is out of date or you don’t have xcode commandline tools installed. Run \
``xcode-select --install`` \
and try again. On new OS X versions, a permissions window will open but isn’t always visible 
if you have other windows open – you may need to hunt for the dialog box to proceed with the xcode installation.

**Trying to install Euterpea or HSoM gives the error: unknown argument: ‘-no-pie’** \
Your xcode version is out of date. If you have a recent version of OSX, run ``xcode-select --install`` to update it. 
If you have an old version of OSX and can’t update xcode, an alternate solution is described here.

**Installing Euterpea fails with the error “xcrun: error: invalid active developer path (…)”** \
This indicates missing command line tools that Haskell Platform depends on. To install these, run:
``xcode-select --install``

**Trying to run a program using HSoM’s MUIs crashes with the error: GLUT Fatal Error: internal error: 
NSInternalInconsistencyException, reason: nextEventMatchingMask should only be called from the Main Thread!** \
This is due to trying to using HSoM’s MUIs in a multithreaded situation. While such applications often are successful on Windows, 
on Mac they experience problems with the GLUT library. While this can limit performance, the only safe way to run a MUI-using 
program on Mac is to stick to a single thread compile with either ghc YourProgram.lhs or ghc -O2 YourProgram.lhs. Avoid using 
fork operations in any code involving MUIs and do not compile with either the rtsopts or threaded flags.

**Trying to run a MUI with MIDI output crashes with a pattern matching exception.** \
This is a known bug that will hopefully be fixed soon, and it is due to trying to list MIDI output devices when there are none available. 
The fix is to make sure you have a synthesizer (like SimpleSynth) or other MIDI output device active before starting the program.
Also, make sure you compile your program with ghc using the instructions under “testing MUIs” further up on this page.

**HSoM’s MUIs crash or the windows hang and are unresponsive.** \
If you are trying to run them from GHCi, try compiling to executable as described in the “Testing HSoM’s MUIs” section further up on this page.
If compiling to executable fails as well, try running the following: \
``cabal install GLUT --ghc-options="-optl-Wl,-framework,GLUT" --reinstall --jobs=1 --force-reinstalls`` \
You may need to reinstall HSoM with cabal install HSoM again afterwards. 
If you still have problems, please report the problems with a complete transcript and OS version information on HSoM’s GitHub issues page.
Although this issue has been fixed on more recent versions of OSX and Haskell Platform, OSX 10.11 users with 
some older versions of Haskell Platform may also need to first disable rootless by running: \
``sudo nvram boot-args="rootless 0"`` \
and then rebooting. See this thread for more information. If you already tried installing Haskell Platform without trying the 
fix above and the installation failed, you should fully uninstall it, disable rootless as above, and then reinstall. 
To uninstall Haskell Platform, run the following (and any additional commands you are prompted for): \
``sudo uninstall-hs``


# Linux-Specific Problems

**Euterpea installation fails with a PortMidi-related error: “missing C library: asound”** \
This is a missing dependency problem. Try running ``apt-get install libasound2-dev``

Please note that Euterpea is not guaranteed to work on Linux. Although Ubuntu usually works, there are too many different distributions to ensure compatibility across everything. For example, NixOS is typically incompatible with Euterpea.
