# Telegram bots scripts and configs

A set of scripts to simplify the execution of telegram bots and, in general, an
 arbitrary set of simple sets of containers
 using `podman-comopse` and `systemd`.

The suggested scripts are more or less compatible with `docker-compose` and can
 be modified for use with `docker`, but are not directly tested with
 `docker-compose`.

# How to add bot?

You may place all scripts in any directory, but the `*@.service` file contains
 the hardcoded `./composectl` location. Therefore, it is desirable to place all
 files in `/opt/telegram-bots` and subdirs.

The owner of the files in this directory can be a non-privileged user, this is
 not important, since in the current version the `*@.service` file does not
 restrict the user used to execute the service
 (TODO: Of course it needs to be fixed).

Each telegram-bot runs as a separate `sysdemd` service. To add a bot you need:

* Create a subdirectory in `/opt/telegram-bots`,
  for example `/opt/telegram-bots/idbot`

* Place in this directory a declarative description for the `podman-compose`
  according to the [compose-spec](https://github.com/compose-spec/compose-spec/blob/master/spec.md).
  In general, there is no limit to the creation of this description. But it's
  good practice to store persistent data in the bot's directory and/or attach
  a description of the permanent storage locations. It is also good practice to
  create health checks for the containers.

* Run a bot using `podman-compose` or `./composectl`

* After this, copy the `*@.service` file to `/etc/systemd/system/`
  and start/enable the service

You don't need to do anything else for `systemd`, and `podman-compose`.
 Logs can be viewed in the journalctl, status of the bot can be found
 using `systemctl`. Everything works the way you expect it, no tricks.

# Usage and Bugs reporting

You are free to use this bunch of scripts if it is suitable to you.
 You are welcome to fix something, if you want.

I expect Issues/PR's not on bot config's, but on the
 systemd+podman-compose solution. Maybe we can make it more universal
 and compatible in the future.

This project is not aims to add all the telegram-bots from the Internet
 it is just my bunch of bots used for my needs. If you can't run anything
 with this set of scripts, please make the issue, I'll try to fix it.
