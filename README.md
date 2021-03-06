# Unix system version information

Print the current Unix system version information.

Syntax:

    unix-system-version-information

Example:

    $ unix-system-version-information
    Unix System Version Information
    timestamp: 2016-09-04T19:32:43Z

    uname -a
    Darwin host.example.com
    16.0.0 Darwin Kernel Version 16.0.0: Thu Aug 18 18:25:11 PDT 2016;
    root:xnu-3789.1.29~5/RELEASE_X86_64 x86_64

    sw_vers
    ProductName:       Mac OS X
    ProductVersion:    10.12
    BuildVersion:      16A304a


## Goals

This script has three goals:

  * Print the OS name, version, build, and related information.

  * Run cross platform on many Unix systems and Unix-like systems.

  * Print information that may be useful for diagnostics and debugging.

This script prints a timestamp, which can be useful for snapshotting
system information during an upgrade process, or at differing times, etc.

This implementation looks for information in these places:

  * The `uname` command.
  * The `sw_vers` command on macOS.
  * The `pkginfo` command on Solaris.
  * The `lsb_release` command on Linux.
  * Files with names including `release`, `version`, `issue`, etc.
  * We welcome more ways of finding information.

This implementation is intended to work on current versions of
many Unix systems and Unix-like systems, using POSIX shell commands.
 
This implementation looks for commands and files suitable for
Annvix, Arch Linux, Arklinux, Aurox Linux, BlackCat, BSD Cobalt,
Chakra, Conectiva, Debian, Fedora / Fedora Core, FreeBSD, FreeEOS,
Gentoo Linux, HLFS, HPUX, Immunix, IYCC, Knoppix, Linux-From-Scratch /
LFS, Linux-PPC, Linux Mint, Apple Macintosh macOS / OS X / Darwin,
Mageia, Mandrake, Mandriva/Mandrake Linux, MkLinux, Novell Linux
Desktop, PLD Linux, RHEL / RHAS / Red Hat Linux, Rubix, Scientific
Linux / ScientificSL / ScientificCERNSLC / ScientificFermiLTS /
ScientificSLF, Slackware, SME Server (Formerly E-Smith), Solaris
SPARC, Sun JDS, SUSE Linux, SUSE Linux ES9, Synology, Tiny Sofa,
Trustix, TurboLinux, Ubuntu Linux, UltraPenguin, UnitedLinux,
VA-Linux/RH-VALE, Yellow Dog.

## uname command

This script calls the `uname` command, which prints the
operating system name plus more system information.

Example on Apple macOS:

    $ uname -a
    Darwin hostname 14.0.0
    Darwin Kernel Version 14.0.0:
    Fri Sep 19 00:26:44 PDT 2014;
    root:xnu-2782.1.97~2/RELEASE_X86_64 x86_64

Example on Oracle Solaris:

    $ uname -a
    SunOS sndcc02.sanjose.ibm.com 5.10 Generic sun4u sparc
    SUNW,Sun-Fire-V490

Example on Ubuntu Linux:

    $ uname -a
    Linux hostname 2.6.35.4-rscloud #8 SMP
    Mon Sep 20 15:54:33 UTC 2010
    x86_64 GNU/Linux


## sw_vers command

The macOS `sw_vers` command prints software version
information, such as the product name and build version.

Example of `sw_vers` running on macOS:

    $ sw_vers
    ProductName:Mac OS X
    ProductVersion:10.10
    BuildVersion:14A389


## lsb_release command

The Linux `lsb_release` command prints distribution 
information, such as the release name, codename, 
description, etc.

Example of `lsb_release` running on Ubuntu Linux:

    $ lsb_release -a 
    No LSB modules are available.
    Distributor ID:    Ubuntu
    Description:       Ubuntu 16.04.1 LTS
    Release:           16.04
    Codename:          xenial


## release version files

Some systems put release version information in a plain text file.

The file is often called "release", "version", "issue", or similar.

The file is stored in a typical location, such as `/etc/version`, or similar.

Examples:

    $ cat /etc/release
    Solaris 10 5/08 s10x_u5wos_10 X86 ...
    Solaris 10 10/09 (Update 8) Patch Bundle applied.

    $ cat /proc/version
    Linux version 4.4.0-34-generic (buildd@lgw01-20) 
    (gcc version 5.3.1 20160413 (Ubuntu 5.3.1-14ubuntu2.1) )
    #53-Ubuntu SMP Wed Jul 27 16:06:39 UTC 2016

    $ cat /etc/issue.net
    Ubuntu 16.04.1 LTS


## Thanks

Thanks for guidance, advice, and improvements:

  * [Linux Mafia FAQ on release files](http://linuxmafia.com/faq/Admin/release-files.html)
  * [andlrc](https://www.reddit.com/user/andlrc)
  * [whetu](https://www.reddit.com/user/whetu)


## Tracking

* Command: unix-system-info
* Version: 3.4.0
* Created: 2014-12-24
* Updated: 2016-09-05
* License: BSD, MIT, GPL
* Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
