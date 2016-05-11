#TCL4DM

###TCL4DM is an implementation of the Tool Command Language for Byond's Dream Maker language.
 
##TCL

Tool Command Language (or TCL (pronounced tickle when not spelled out)) is a language designed from the ground up to be expandable, and to be embeddable into other languages. It has a simple syntax with 11 simple rules.

Current plans are to implement TCL8.5, but this may change to TCL8.6

##DM

Dream Maker (or DM) is the language of the Build Your Own Net Dream (or byond, pronounced beyond) game engine. It is designed for ease of use when making tile and sprite based multiplayer games.

We will be designing this to target version 507.

***

TCL4DM is currently not even in alpha, and we aren't accepting code related PRs (but feel free to fix my typos in the meta documents like this one, but after the parser and core framework is done, we will be seeking out brave programmers to help implement all of tcl's internal commands as well as develop ways of interacting with the game world from within the language. Feel free to read the Guide to contributing inside of CONTRIBUTING.md in the mean time.

It will be designed to be flexible in ways that allow it to be used as the scripting language of in game machinery/structures by players, or as a way for admins to design scripts to manipulate the game world and state in ways that would otherwise be prohibitive to do by hand.

In game objects will be able to spawn their own TCL interpreter, add commands to it that link directly to a byond proc on the object, and even hook into built in commands.

