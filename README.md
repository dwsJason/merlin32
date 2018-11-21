# Merlin32
The Merlin 32 assembler for the Apple II from Brutal Deluxe Software

## Build from Source and Install

There are 2 different make files.

1. GNUmakefile - Used for Mac, Linux & BSD UNIX
2. Makefile - Used for Windows with nmake and MSVC

The build process is too different between Windows and the other platforms
to be done with the same make file. Using the current make file naming
convention allows the builder to use the same workflow regardless of the
platform. GNU make on Mac, Linux and BSD UNIX automatically looks for 
GNUmakefile first and will ignore Makefile if GNUmakefile exists. Likewise,
nmake on Windows will ignore GNUmakefile and use Makefile instead.

### Mac, Linux, & BSD UNIX

#### Build with default install loaction

1. <code>cd Source</code>
2. <code>make</code>
3. <code>sudo make install</code>

This will install it into these locations:

<code>/usr/local/bin/merlin32</code><br>
<code>/usr/local/share/merlin32/asminc/*.Mac.s</code>

#### Alternate Install Location

The default install location (PREFIX) is /usr/local.
You can change the install location like this. Make sure you specify
the PREFIX on both steps.

1. <code>make PREFIX=/opt/merlin32</code>
2. <code>sudo make PREFIX=/opt/merlin32 install</code>

This would install to:

<code>/opt/merlin32/bin/merlin32</code><br>
<code>/opt/merlin32/share/merlin32/asminc/*.Mac.s</code>

Then you would have to manually add to your PATH because that bin directory
is not normally in the PATH like /usr/local/bin is.

### Windows

#### Install

1. Start a Visual Studio Command Prompt from the Start Menu.
2. Change to the Source directory of the merlin32 extracted archive.
3. <code>nmake</code>
4. <code>nmake install</code>

This will install it into C:\Users\You\Applications\merlin32 and will
automatically put the bin directory into the path. You'll have to start
a new Command Prompt to see it in the path.

The install copies to these locations:

<code>C:\Users\You\Applications\merlin32\bin\merlin32.exe</code><br>
<code>C:\Users\You\Applications\merlin32\asminc\*.Macs.s</code>

#### Options

To get it to install into "C:\Program Files" would require a setup application
that would be able to do privilege escalation. That is not currently supported. But you could install into a directory like C:\opt because that is not protected like "C:\Program Files". To do
that build it like this:

1. <code>nmake clean</code>
2. <code>nmake PREFIX=C:\opt\merlin32 install</code>

On Windows, the bin directory is automatically added to the PATH regardless
of where it is installed. This is done with the script 
merlin32\Scripts\addtopath.bat.

#### Uninstall

The merlin32\Scripts\uninstall.bat script will uninstall it from the
standard folder C:\Users\You\Applications\merlin32.

If you installed it to another location, just delete that directory.
For example:

<code>rmdir /s C:\opt\merlin32</code>

## Running

Invoking Merlin32 should be the same on all platforms.

After running the above install step, merlin32 should be in your PATH.

The location of the macro library files is compiled into the executable
so it is optional on the command line. You can run it with or without
specifying the macro library directory. So it is backward compatible with
the original release.

<code>$ merlin32 ~/git/merlin32/Library skynet.s</code><br>
<code>$ merlin32 skynet.s</code>  (Will automatically use PREFIX/share/merlin32/asminc)

