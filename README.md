# spideroak-init
This project provides tools for starting and stopping the SpiderOak service
(https://www.spideroak.com) from a SysV init or systemd environment.

* This project includes the following files:
    * COPYING -- the license (public domain where applicable, CC0 elsewhere)
    * README.md -- this file
    * spideroak -- a SysV init script
    * SpiderOak -- the configuration file
    * spideroak@.service -- a systemd service file

## Installation
To install on a system using SysV init scripts, copy the file 'spideroak' to
/etc/init.d/spideroak and the file 'SpiderOak' to /etc/sysconfig/SpiderOak . (If
/etc/sysconfig does not exist on your system - for example, Debian and Ubuntu
installations - copy it to the appropriate directory for your operating system
and edit /etc/init.d/spideroak to point to the correct location.)

To install on a system using systemd, copy the file 'spideroak@.service' to
/usr/lib/systemd/system/spideroak@.service and the file 'SpiderOak' to
/etc/sysconfig/SpiderOak . 

## Configuration
Configuration is handled through /etc/sysconfig/SpiderOak. Both systemd and SysV
init will use the SPIDEROAKOPTS setting to pass options to the SpiderOak
process. '--headless' is automatically included and so does not need to be
specified in SPIDEROAKOPTS.

The SysV init script also uses the SPIDEROAKUSER setting to specify the user
that SpiderOak should run under. If more than one (space-delimited) account is
given, a separate SpiderOak process will be launched for each user. The SysV
init script also uses the SPIDEROAKCMD setting to determine the location of the
executable. It should not be necessary to use this setting under normal
circumstances.

**Note: the scripts and configuration do not perform any sanity-checking on your
behalf. For the security of your system and data, ensure that files have the
proper ownership and permissions.**

## Multi-user support
For systemd, the provided service file is a template. The text between the @ and
. indicate the user name that SpiderOak should be launched as. Thus to start
SpiderOak for both user 'funnel' and user 'fiasco' you would run

    systemctl spideroak@funnel.service start
    systemctl spideroak@fiasco.service start

For SysV init, multiple users can be listed (space-separated) in the
/etc/sysconfig/SpiderOak file. For example

    SPIDEROAKUSER="funnel fiasco"

Setting per-user SPIDEROAKOPTS is not currently supported.
