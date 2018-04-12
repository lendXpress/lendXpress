
LendXpress Official Development Repo
==================================
### LendXpress Resources
* Client and Source:
* Documentation: 

* Help: 
SOCIAL MEDIA LINKS

Website: https://ico.lendxpress.co/
Twitter: https://twitter.com/Lendxpresss
Telegram: https://t.me/LendXpress
GitHub: https://github.com/lendXpress/


Repo Guidelines
================================

* Developers work in their own forks, then submit pull requests when they think their feature or bug fix is ready.
* If it is a simple/trivial/non-controversial change, then one of the development team members simply pulls it.
* If it is a more complicated or potentially controversial change, then the change may be discussed in the pull request, or the requester may be asked to start a discussion in the [LendXpress Forum] for a broader community discussion. 
* The patch will be accepted if there is broad consensus that it is a good thing. Developers should expect to rework and resubmit patches if they don't match the project's coding conventions (see coding.txt) or are controversial.
* From time to time a pull request will become outdated. If this occurs, and the pull is no longer automatically mergeable; a comment on the pull will be used to issue a warning of closure.  Pull requests closed in this manner will have their corresponding issue labeled 'stagnant'.
                                  
								    ********************BUILDING LENDXPRESS**************************
								
	
	
	===================WINDOWS BUILD NOTES===================


Compilers Supported
-------------------
TODO: What works?
Note: releases are cross-compiled using mingw running on Linux.


Dependencies
------------
Libraries you need to download separately and build:

                default path               download
OpenSSL         \openssl-1.0.1b-mgw        http://www.openssl.org/source/
Berkeley DB     \db-4.8.30.NC-mgw          http://www.oracle.com/technology/software/products/berkeley-db/index.html
Boost           \boost-1.47.0-mgw          http://www.boost.org/users/download/
miniupnpc       \miniupnpc-1.6-mgw         http://miniupnp.tuxfamily.org/files/

Their licenses:
OpenSSL        Old BSD license with the problematic advertising requirement
Berkeley DB    New BSD license with additional requirement that linked software must be free open source
Boost          MIT-like license
miniupnpc      New (3-clause) BSD license

Versions used in this release:
OpenSSL      1.0.1b
Berkeley DB  4.8.30.NC
Boost        1.47.0
miniupnpc    1.6


OpenSSL
-------
MSYS shell:
un-tar sources with MSYS 'tar xfz' to avoid issue with symlinks (OpenSSL ticket 2377)
change 'MAKE' env. variable from 'C:\MinGW32\bin\mingw32-make.exe' to '/c/MinGW32/bin/mingw32-make.exe'

cd /c/openssl-1.0.1b-mgw
./config
make

Berkeley DB
-----------
MSYS shell:
cd /c/db-4.8.30.NC-mgw/build_unix
sh ../dist/configure --enable-mingw --enable-cxx
make

Boost
-----
DOS prompt:
downloaded boost jam 3.1.18
cd \boost-1.47.0-mgw
bjam toolset=gcc --build-type=complete stage

MiniUPnPc
---------
UPnP support is optional, make with USE_UPNP= to disable it.

MSYS shell:
cd /c/miniupnpc-1.6-mgw
make -f Makefile.mingw
mkdir miniupnpc
cp *.h miniupnpc/

LendXpress
-------
DOS prompt:
cd \LendXpress\src
mingw32-make -f makefile.mingw
strip LendXpress.exe


	 ================ OSX BUILD NOTES================
Tested on 10.5 and 10.6 intel.  PPC is not supported because it's big-endian.

All of the commands should be executed in Terminal.app.. it's in
/Applications/Utilities

You need to install XCode with all the options checked so that the compiler and
everything is available in /usr not just /Developer I think it comes on the DVD
but you can get the current version from http://developer.apple.com


1.  Clone the github tree to get the source code:

git clone git@github.com:rat4/LendXpress.git LendXpress

2.  Download and install MacPorts from http://www.macports.org/

2a. (for 10.7 Lion)
    Edit /opt/local/etc/macports/macports.conf and uncomment "build_arch i386"

3.  Install dependencies from MacPorts

sudo port install boost db48 openssl miniupnpc

Optionally install qrencode (and set USE_QRCODE=1):
sudo port install qrencode

4.  Now you should be able to build LendXpress:

cd LendXpress/src
make -f makefile.osx

Run:
  ./LendXpress --help  # for a list of command-line options.
Run
  ./LendXpress -daemon # to start the LendXpress daemon.
Run
  ./LendXpress help # When the daemon is running, to get a list of RPC commands

								  
								 ================ UNIX BUILD NOTES================


To Build
--------

cd src/
make -f makefile.unix            # Headless LendXpress

See readme-qt.rst for instructions on building LendXpress QT,
the graphical LendXpress.

Dependencies
------------

 Library     Purpose           Description
 -------     -------           -----------
 libssl      SSL Support       Secure communications
 libdb       Berkeley DB       Blockchain & wallet storage
 libboost    Boost             C++ Library
 miniupnpc   UPnP Support      Optional firewall-jumping support
 libqrencode QRCode generation Optional QRCode generation

Note that libexecinfo should be installed, if you building under *BSD systems. 
This library provides backtrace facility.

miniupnpc may be used for UPnP port mapping.  It can be downloaded from
http://miniupnp.tuxfamily.org/files/.  UPnP support is compiled in and
turned off by default.  Set USE_UPNP to a different value to control this:
 USE_UPNP=-    No UPnP support - miniupnp not required
 USE_UPNP=0    (the default) UPnP support turned off by default at runtime
 USE_UPNP=1    UPnP support turned on by default at runtime

libqrencode may be used for QRCode image generation. It can be downloaded
from http://fukuchi.org/works/qrencode/index.html.en, or installed via
your package manager. Set USE_QRCODE to control this:
 USE_QRCODE=0   (the default) No QRCode support - libqrcode not required
 USE_QRCODE=1   QRCode support enabled

Licenses of statically linked libraries:
 Berkeley DB   New BSD license with additional requirement that linked
               software must be free open source
 Boost         MIT-like license
 miniupnpc     New (3-clause) BSD license

Versions used in this release:
 GCC           4.9.0
 OpenSSL       1.0.1g
 Berkeley DB   5.3.28.NC
 Boost         1.55.0
 miniupnpc     1.9.20140401

Dependency Build Instructions: Ubuntu & Debian
----------------------------------------------
sudo apt-get install build-essential
sudo apt-get install libssl-dev
sudo apt-get install libdb++-dev
sudo apt-get install libboost-all-dev
sudo apt-get install libqrencode-dev

If using Boost 1.37, append -mt to the boost libraries in the makefile.


Dependency Build Instructions: Gentoo
-------------------------------------

emerge -av1 --noreplace boost openssl sys-libs/db

Take the following steps to build (no UPnP support):
 cd ${DavorCoin_DIR}/src
 make -f makefile.unix USE_UPNP=
 strip LendXpress


Notes
-----
The release is built with GCC and then "strip LendXpress" to strip the debug
symbols, which reduces the executable size by about 90%.


miniupnpc
---------
tar -xzvf miniupnpc-1.6.tar.gz
cd miniupnpc-1.6
make
sudo su
make install


Berkeley DB
-----------
You need Berkeley DB. If you have to build Berkeley DB yourself:
../dist/configure --enable-cxx
make


Boost
-----
If you need to build Boost yourself:
sudo su
./bootstrap.sh
./bjam install


Security
--------
To help make your LendXpress installation more secure by making certain attacks impossible to
exploit even if a vulnerability is found, you can take the following measures:

* Position Independent Executable
    Build position independent code to take advantage of Address Space Layout Randomization
    offered by some kernels. An attacker who is able to cause execution of code at an arbitrary
    memory location is thwarted if he doesn't know where anything useful is located.
    The stack and heap are randomly located by default but this allows the code section to be
    randomly located as well.

    On an Amd64 processor where a library was not compiled with -fPIC, this will cause an error
    such as: "relocation R_X86_64_32 against `......' can not be used when making a shared object;"

    To build with PIE, use:
    make -f makefile.unix ... -e PIE=1

    To test that you have built PIE executable, install scanelf, part of paxutils, and use:
    scanelf -e ./LendXpress

    The output should contain:
     TYPE
    ET_DYN

* Non-executable Stack
    If the stack is executable then trivial stack based buffer overflow exploits are possible if
    vulnerable buffers are found. By default, LendXpress should be built with a non-executable stack
    but if one of the libraries it uses asks for an executable stack or someone makes a mistake
    and uses a compiler extension which requires an executable stack, it will silently build an
    executable without the non-executable stack protection.

    To verify that the stack is non-executable after compiling use:
    scanelf -e ./LendXpress

    the output should contain:
    STK/REL/PTL
    RW- R-- RW-

    The STK RW- means that the stack is readable and writeable but not executable.

				