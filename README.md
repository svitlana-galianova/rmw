[![Build Status](https://travis-ci.org/andy5995/rmw.svg?branch=master)](https://travis-ci.org/andy5995/rmw)
[![Build Status](https://semaphoreci.com/api/v1/andy5995/rmw/branches/master/badge.svg)](https://semaphoreci.com/andy5995/rmw)

# rmw v0.4.04 (development)

rmw is an OS portable cli trash can utility written in C. It can send
files to your "Desktop" trash, or a completely separate folder. It can
also: restore files; permanently delete files that were rmw'ed more
than xx number of days ago; skip files or directories that have a
"PROTECT" directive in the configuration file; and append a unique
string to the filenames so they won't be overwritten (duplication
protection).

Web site: https://github.com/andy5995/rmw/wiki

This is the README for the development version of rmw. It may mention
features that aren't included in the last release, or differ in other
ways. The README from the last release is at
https://github.com/andy5995/rmw/blob/v0.4.03/README.md

Anyone interested in this project is welcome to join the [chat
room](https://join.slack.com/t/removetowaste/shared_invite/enQtMjU3NTA0NTI2OTgzLTkzMzQxNDhjYzlkM2UxMTA2MzJjNWYyZjAyYzkyNWNmZjJmYWZmYjUyODk2NzNkNzBhMzFjOGZkMTg2MzAxMTM).

If you would like to help translate the man page or the output messages
for this program, please see the [Translating wiki
page](https://github.com/andy5995/rmw/wiki/Translating).

## Required libraries

libncurses5

If you are building from source, you will need the libncurses(5 or 6)-dev
package from your operating system distribution.

## Installation

### With superuser privileges:

Use `./configure --help` to view available compile-time options.

    ./configure --prefix=/usr --sysconfdir=/etc
    make
    make install

If the --prefix and --sysconfdir options are omitted, "/usr/local" will be
used instead. If you are using **MacOSX** and have problems installing to
/usr/bin, try omitting those two options.

### As a normal user:

    ./configure --prefix=$HOME/usr
    make
    make install

rmw will be installed to $HOME/usr/bin and the configuration file will be
copied to $HOME/usr/etc

### Pre-built binary packages

Packages for some operating systems are available on the
[Downloads](https://github.com/andy5995/rmw/releases) page

## Uninstall / Cleaning up

    make uninstall
    make distclean
```
man pages are now available in the following languages:

    * de
    * en
    * es
    * fi
    * ne
    * nl_NL
    * pl
    * pt_BR

If you installed rmw as a normal user, this next step can be skipped.

After rmw is installed, create the user configuration directory by typing
'rmw' and hitting enter. Afterward, it's recommended to copy /etc/rmwrc (or
/usr/local/etc/rmwrc) to $HOME/.config/rmw and then rename it to 'config':

'cd ~/.config/rmw'
'~/.config/rmw$ cp /etc/rmwrc .'
'~/.config/rmw$ mv rmwrc config'

Then edit the file to suit your needs.

At some point, rmw will automatically create a 'lastpurge' and 'lastrmw'
in that same directory.

== Configuration File ==

Documentation explaining the configuration can be found in 'etc/rmwrc'

Waste folders will be created automatically. (e.g. if '$HOME/trash.rmw'
is listed in the config file, these 3 directories will be created:
$HOME/trash.rmw
$HOME/trash.rmw/files
$HOME/trash.rmw/info

If one of the WASTE folders is on removable media, then the user has the
option of appending ',removable' (details in etc/rmwrc).

== Features and Options ==

-h, --help
-t, --translate           display a translation of the configuration file
-c, --config filename     use an alternate configuration
-l, --list                list waste directories
-g, --purge               run purge even if it's been run today
-o, --orphaned            check for orphaned files (maintenance)
-f, --force               allow purge to run
-B, --bypass              bypass directory protection
-v, --verbose             increase output messages
-w, --warranty            display warranty
-V, --version             display version and license information


	===] Restoring [===

-z, --restore <wildcard filename(s) pattern>
-s, --select              select files from list to restore
-u, --undo-last           undo last ReMove

== Purging ==

If purging is 'on', rmw will permanently delete files from the folders
specified in the configuration file after 'x' number of days. Purging can be
disabled by using 'purge_after = 0' in configuration file. rmw will only check
once per day if it's time to purge (use -g to check more often).

Purge requires -f (--force) to run.

To skip that requirement, add the line

force_not_required

to your configuration file.

The day of the last purge is stored in $HOME/config/rmw/lastpurge

== Empty the Trash ==

To empty the trash completely, rmw can use the environmental variable
RMWTRASH. Usage:
RMWTRASH=empty rmw -fg

== -z option ==

To restore a file, or multiple files, specify the path to them in in the
<WASTE>/files folder (wildcards ok).
e.g. 'rmw -z ~/.local/share/Trash/files/foo*'

Files can also be restored using only the basename, from within any directory.
NOTE: That feature will not process wildcards unless the user is in a
<WASTE>/files folder and the filespec actually exists in the present working
directory.

== Protected directories ==

If 'PROTECT = /home/andy' is specified in the config file, /home/andy, and all
dirs and files beneath it will be "protected"; they will be skipped, and this
warning will be displayed:

"File is in protected directory: <filename/dir>"

WASTE folders and the rmw configuration/data directory are protected by
default (there is no need to add a 'PROTECT =' line for them.

Protection can by bypassed using -B

== -t, --translate ==

If a translation of the configuration file is available in your native
language is available, it will be displayed.

(If you would be interested in adding a translation, please visit
https://github.com/andy5995/rmw/wiki/Translating)

== -f, --force ==
rmw will normally refuse to purge directories if they contain non-writable
subdirectories. You can use -f 2 times if you ever see a message that tells
you "permission denied; directory still contains files" (e.g. rwm -gff).

```
