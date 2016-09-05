# Unix system version inofmration

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

  * Run reliably cross platform, to work well on all flavors of Unix.

  * Print information that may be useful for diagnostics and debugging.

This script prints a timestamp, which can be useful for snapshotting
system information during an upgrade process, or at differing times, etc.

This implementation looks for information in these places:

  * The `uname` command.
  * The `lsb_release` command on Linux.
  * The `sw_vers` command on macOS.
  * Distro files such as `/etc/*-release`, `/etc/*_version`, `/proc/version`, `/etc/issue.net`.
  * We welcome more ways of finding information.


## uname command

This script calls the `uname` command, which prints the
operating system name plus more system information.

Example of `uname` running on Ubuntu Linux:

    $ uname -a
    Linux hostname 2.6.35.4-rscloud #8 SMP
    Mon Sep 20 15:54:33 UTC 2010
    x86_64 GNU/Linux

Example of `uname` running on macOS:

    $ uname -a
    Darwin hostname 14.0.0
    Darwin Kernel Version 14.0.0:
    Fri Sep 19 00:26:44 PDT 2014;
    root:xnu-2782.1.97~2/RELEASE_X86_64 x86_64


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


## sw_vers command

The macOS `sw_vers` command prints software version
information, such as the product name and build version.

Example of `sw_vers` running on macOS:

    $ sw_vers
    ProductName:Mac OS X
    ProductVersion:10.10
    BuildVersion:14A389


## /etc/*-release file

Some Unix systems store information in a text file in a typical location.

Examples:

    $ cat /etc/debian_version
    stretch/sid

    $ cat /etc/mandrake-release
    ...TODO...

    $ cat /etc/redhat-release
    Red Hat Enterprise Linux Server release 6.8 (Santiago)

    $ cat /SuSE-release
    ...TODO...

    $ cat /proc/version
    Linux version 4.4.0-34-generic (buildd@lgw01-20) 
    (gcc version 5.3.1 20160413 (Ubuntu 5.3.1-14ubuntu2.1) )
    #53-Ubuntu SMP Wed Jul 27 16:06:39 UTC 2016

    $ cat /etc/issue.net
    Ubuntu 16.04.1 LTS


## TODO

* Add example of `redhat-release` file.
* Add example of more Unix flavors, such as AIX, Solaris, etc.


## Thanks

Thanks for advice and improvements:

  * [andlrc](https://www.reddit.com/user/andlrc)
  * [whetu](https://www.reddit.com/user/whetu)


## Tracking

* Command: unix-system-info
* Version: 3.1.0
* Created: 2014-12-24
* Updated: 2016-09-04
* License: BSD, MIT, GPL
* Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
