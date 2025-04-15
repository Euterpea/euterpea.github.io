# Getting Started with Euterpea

Euterpea is a cross-platform, domain-specific language for computer music applications embedded in the Haskell programming language. Euterpea is a wide-spectrum language, suitable for high-level music representation, algorithmic composition, music analysis, working with MIDI, low-level audio processing, sound synthesis, and virtual instrument design.

# About

Euterpea is a domain-specific language, embedded in the functional language Haskell, for computer music composition and development. The name Euterpea is derived from Euterpe, who was one of the nine Greek Muses (goddesses of the arts), specifically the Muse of Music.

Euterpea is a descendant of Haskore and HasSound, and is intended for both educational purposes as well as serious computer music applications. Euterpea is a wide-spectrum language, suitable for high-level music representation, algorithmic composition, and analysis; mid-level concepts such as MIDI; and low-level audio processing, sound synthesis, and instrument design.

# Compatibility

- OS: Windows 7+, OS X 10.12+, some Linux distributions (requires ALSA)
- Recommended GHC versions: 8.2.2 – 9.4.6 depending on operating system
  - Windows: 8.2.2 – 8.10.5
  - Mac: 8.2.2 – 9.4.6
  - Linux: varies a lot by distribution – 8.x usually works but Euterpea’s compatibility is not guaranteed with all distributions and some trial and error may be required to get it working.

If you already have GHC but it’s outside any of the ranges listed above, Euterpea may still work – give it a try before installing a different version.

# Getting Started with Euterpea
Here’s what you need to do to install Euterpea for the first time and play your first note in four general steps: installing Haskell, installing Euterpea, setting up a synthesizer, and installing HSoM.

## Step 1: Install Haskell
Install Haskell for your operating system. Ideally use one of the GHC versions listed at the top of the page. Each OS category has its own caveats either before or after installation:

Mac: you may need to install or update xcode first if you get cryptic install errors.
Windows: check your default installed GHC version if using ghcup! You may need to manually downgrade to 8.10.5 to avoid installation errors (using “ghcup install ghc 8.10.5”).
Linux: you must install ALSA (ex: sudo apt-get install libasound2-dev)

## Step 2: Install Euterpea
Download or clone the Euterpea2 repository on GitHub. If downloading as a ZIP file, unzip it. Open a command prompt (Windows) or terminal (Mac/Linux) and cd into the repository folder where the euterpea.cabal file is located. Run the following commands:

```
cabal update
cabal v1-install --allow-newer
```

Older ghc/cabal version users: if you run into weird errors about finding compatible package versions, try using
``cabal v1-update``
instead and then re-running the install command.

If you can’t get Euterpea to install with the commands listed here, check the troubleshooting page.

## Step 3: Setup a Synth and Test Euterpea

**Mac/Linux users**: install a MIDI software synthesizer, such as VMPK, SimpleSynth, or Fluidsynth. Make sure it’s running before you start Euterpea in GHCi. With VMPK for Mac, make sure “omni” is enabled and that it’s using CoreMidi (not Network).

**Windows users**: typically Windows will already have a generic MIDI synth installed and you can simply move on to testing Euterpea with GHCi. If you don’t have the Windows GM synth for whatever reason, you can try Coolsoft’s VirtualMIDISynth. Make sure to have it running with instruments loaded before starting GHCi.

Open a *new* command prompt, powershell, or terminal and run the following commands.

```
ghci
import Euterpea
play $ c 4 qn
You should hear a note play if your synth is configured correctly. If you don’t, check the Setting Up MIDI and Troubleshooting pages.
```

**Important:** do *not* start ghci from within the euterpea repository folder where you performed the installation! If you attempt to import Euterpea from the folder containing etuerpea.cabal, you'll get errors.

## Step 4: Install HSoM (Optional)

If you also want HSoM, which is the companion library for the Haskell School of Music textbook, you can install it similarly to Euterpea. Download/clone the the HSoM repository on GitHub, cd into the repository folder (where hsom.cabal is), and run the ``cabal v1-install`` command as you did for Euterpea.

Mac users: to use HSoM’s musical user interfaces (MUIs), you must compile to executable rather than using the interpreter. There’s an example of how to do this on the Compiling to Executable page.

Now you’re ready to head to the Tutorials and Examples pages to learn about how to use Euterpea and try out some existing code. Once you’re ready to start building your own programs with Euterpea, head to the API Documentation for more information on Euterpea’s features.

Having installation trouble or don’t hear any sound?
Check out the Troubleshooting page for a list of solutions for common problems organized by OS and category. For sound-related problems, you can also check out the Setting up MIDI page.

Looking for a text editor to use with Haskell & Euterpea?
Here are some suggestions:

- Notepad++ (Windows only)
- Atom with a Haskell plugin (Windows/Mac/Linux)

Or check out this extensive list of editor options: https://wiki.haskell.org/Editors

# Questions/Comments

Please send questions and comments related to Euterpea to Donya Quick (donyaquick@gmail.com) but please read the FAQ below first to see if your question is answered there first! Donya Quick is the current maintainer of the Euterpea and HSoM libraries.

# FAQ

- **Is there a textbook corresponding to Euterpea?** Yes, The Haskell School of Music (HSoM) is a textbook by Paul Hudak and Donya Quick that is about Euterpea.

- **Is Euterpea still under development?** No. Euterpea won’t be changed or added to except for possible future compatibility and/or bug fixes that do not affect its functionality. It will remain compatible with what’s in the HSoM textbook.

- **Can I contribute to Euterpea?** No. Euterpea is open-source but not open to community contributions. However, you are free to do what you want with your own local copy. You can also fork the repository and build on it under your own account.

- **I found a bug or am having installation trouble with Euterpea/HSoM; how do I get help?** First check the Troubleshooting page. Next, check the issues page for the repository to see if it’s a known issue with a solution. If it’s something new, you can either email the Euterpea maintainer (Donya Quick) or create a new issue post. Do not use the pull requests feature on github to propose solutions (pull requests are ignored).

- **I’m having trouble installing Haskell/GHC; where can I get help?** The installation process for Haskell has changed a lot in the last few years, having switched from all-in-one installers to version managers (Chocolatey, GHCup, etc.). Your best bet is to contact the maintainers of the particular version manager you’re using to install GHC.

- **Who created Euterpea?** Euterpea was created by Paul Hudak and the Yale Haskell Group (which no longer exists). The library is currently maintained by Donya Quick, who started helping with it in 2008 and became the primary maintainer in 2015.

  
