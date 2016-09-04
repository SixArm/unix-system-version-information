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

Goals:

  * Print the OS name, version, build, and related information.

  * Work cross platform, to handle all flavors of Unix.

  * Print information that may be useful for diagnostics and debugging.

This script prints a timestamp, which can be useful for snapshotting
system information during an upgrade process, or at differing times, etc.

This implementation looks for information in these places:

  * The `uname` command.
  * The `lsb_release` command on Linux.
  * The `sw_vers` command on macOS.
  * The `redhat-release` file on RedHat.
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

## /etc/redhat-release file

The RedHat operating system stores information in the
file `/etc/redhat-release` as plain text.

Example of `/etc/redhat-release` file:

    $ cat /etc/redhat-release
    ...TODO...

## TODO

* Add example of `redhat-release` file.
* Add example of more Unix flavors, such as AIX, Solaris, etc.


## Tracking

* Command: unix-system-info
* Version: 3.0.0
* Created: 2014-12-24
* Updated: 2016-09-02
* License: BSD, MIT, GPL
* Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
