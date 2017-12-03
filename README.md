# update-o-matic

I wanted a single, cross-platform way to say "Apply all updates in a reasonably
safe and sane manner".  It seems like most update commands require several
discrete commands: clean up, update DB, ACTUALLY update, etc.
Over the years, I've written scripts for most of the
operating systems that I run at home. This is an effort to merge them into
one script that can be pulled down and run from any OS that supports bash.

I wanted scripts that could be run nightly from cron on servers, and scripts
that could be run by non-technical relatives on the desktop. Therefore, the
emphasis is on safety rather than efficiency.

## Requirements
1. bash
2. ability to run as root (or equivalent, like sudo)
3. The uname command must exist
4. If you're running Linux, lsb_release must be installed to detect which
   distribution you're running. Efforts are in progress to remove this
   dependency.

## General update order
1. Update third-party repos or tools that run on top of the OS. Macports, etc.
2. Run any OS cleanup, fix, or check commands. If possible, the script should
   abort if this step fails.
3. Sync update databases and get list of possible updates.
4. Download and apply updates. Avoid experimental or not-recommended updates.
5. If reboot flag is set, reboot after 5 minutes. In the warning message,
   give cancellation instructions, just in case anyone's using the server.

## Supported Operating Systems (so far!)
* Linux variants
  * CentOS
  * Debian
  * Fedora
  * Raspbian
  * Ubuntu
* Darwin (a.k.a. OS X)
  * with or without Macports

## How to install and use
* go to wherever you store source code. Maybe /usr/local/src
* git clone https://github.com/brokengoose/update-o-matic.git
* sudo bash update-o-matic/update-o-matic.sh
* When it's time for updates, cd update-o-matic; git pull

## Known Issues

I'm learning git as I do this. Every change is currently being pushed to the
sole master branch, which is VERY dangerous. Things may break at any moment.

This is currently used and reasonably well tested in my own environment, but
I haven't tested as much in different environments or from pristine installs.
There are probably bugs.

Script assumes that current update tools are in use. For example, dnf on Fedora.
For some operating systems, it might be necessary to dig more into versions
to determine which tool is most appropriate. I thought about falling back to
checking for rpm, deb, etc., but there are a lot of tools out there like alien
that make the situation complicated.


