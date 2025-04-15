# Getting Started & Examples

Once you have Euterpea and possibly HSoM installed, it’s a good idea to try some really simple things first. If you have any trouble with these, please take a look at the [troubleshooting page](https://euterpea.github.io/troubleshooting).

## Play Some Notes

**Mac/Linux users: open your synthesizer!** It must be running first to hear sound from Euterpea.

- Open a command prompt or terminal and run ``ghci`` to start the Haskell interpreter.
- Run import Euterpea and wait for all of the modules to load.
- Run ``play $ c 4 qn`` and listen. You should hear a single tone.
- Want more notes? Try this: \
``play $ line [c 4 qn, c 4 qn, g 4 qn, g 4 qn, a 4 qn, a 4 qn, g 4 hn]`` \
Recognize the melody?


## Notes from a Musical GUI (Requires the HSoM Library)

**Mac/Linux users: make sure your synthesizer is open first!**

- Open a command prompt or terminal and start ghci as above. 

- Run ``import HSoM.Examples.MUIExamples2`` and wait for all of the modules to load.

- Run ``bifurcate`` and wait for a window to pop up (it can take a few seconds to load fully).
You should see a bunch of sliders an text fields with changing values, and you should hear notes periodically.
Move the sliders to hear some crazy stuff.

## Examples

A collection of supplemental code examples is available on GitHub:
[https://github.com/Euterpea/Euterpea2-Examples](https://github.com/Euterpea/Euterpea2-Examples)
These are different from the examples covered in the Haskell School of Music textbook. 
Download the examples and try editing them to explore how the changes affect what you hear – 
experimentation is one of the best ways to learn a new library! 
You can also check out the Examples folder of the HSoM library, which contains all of the code examples from the textbook, 
but without the accompanying descriptions.
Please note that these examples are not meant to fully replace the textbook or other basic tutorials on the 
Haskell programming language as a means of learning Haskell and Euterpea.

## Larger Programs

**[HaskellOx](https://github.com/donya/HaskellOx)** – a program that routs MIDI messages between devices and demonstrates two methods for 
implementing this functionality. The linked zip file includes both the source and a compiled executable for Windows. 
See the batch file for the best compilation method.

## Haskell Tutorials

The Haskell School of Music textbook offers a simultaneous introduction to the Haskell programming language and the Euterpea library. 
However, that’s not the only way to learn the language and library. You can follow some other online Haskell tutorials to familiarize yourself 
with the basic syntax of the language, then take a look at the Euterpea API pages, and browse through the code in the Euterpea library itself 
(all of which is open source). Some useful online tutorials are linked to below.

- Online tutorial: [Learn You a Haskell for Great Good!](http://learnyouahaskell.com/introduction)
- Online tutorial: [How to Learn Haskell](https://acm.wustl.edu/functional/haskell.php)
- PDF document: [A Gentle Introduction to Haskell](https://www.haskell.org/tutorial/haskell-98-tutorial.pdf)
- PDF document: [Yet Another Haskell Tutorial](https://www.umiacs.umd.edu/~hal/docs/daume02yaht.pdf) (more detailed than the one above)
