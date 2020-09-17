# raspi-smarthub
Raspberry Pi monitoring stack with influxdb and grafana.

> This is mainly a documentation for me on what to install but it might be useful for someone else too. Eventually this will be converted to an ansible playbook but for now it's just text instructions.

## What you'll get
This installs the TIG stack (Telegraf, InfluxDB, Grafana) on a Raspberry PI 1 B+ (armv6hf) with some dashboards (displaying smart plug measures, displaying speedtest results).

## Basic Assumptions
Throught this guide I will make some basic assumptions that are applicable for all components, therefore I will explain them once here. Besides from that components can be installed separately and don't depend on each other.

### Operating system
I installed RaspiOS Buster on my Raspberry Pi

### Git
Install git with `sudo apt -y install git` if you don't have already.

### Software installation
I prefer to use the vendor distribution instead of the software that comes packaged with the operating system because they often are a few releases behind. If available I prefer vendor apt repositories because they combine the benefit of easy installation with `apt -y install <package-name>` but are the most recent version. If these packages are not available from the vendor see the next section.

### Directory structure for software not included in the repositories
If a software is not available through official sources I use the following convention:

For a package named `<package-name>` create a user and group `<package-name`. That user will own all files and processes belonging to that package.
```
sudo groupadd <package-name>
sudo useradd <package-name> -g <package-name> -s /usr/sbin/nologin
```

The directory structure looks alot like the usual filesystem, but it's scoped to `<package-name>` so everything belonging to a package is in the same directory.
Additional I like all binaries to `/opt/bin/<binary-name>` so I only need to add `/opt/bin` to path instead of each individual binary.

```shell script

```

```
/
|--opt
    |--<package-name>
        |--bin
            |-- <package-bin> # One or more binaries for that package
        |--var # data for that package like database, etc.
        |--etc # configuration for the package
    |--bin
      |<package-bin> #linked binaries from /opt/<package-name> so you only need to export this dir in $PATH
```
Add the following to your ~/.profile to include /opt/bin in your $PATH
```
# set PATH so includes /opt/bin if it exists
if [ -d "/opt/bin" ] ; then
    PATH=$PATH:/opt/bin
fi
```
and run `source .profile` to activate the changes

It has the following benefits:
* simple uninstallation, just remove /opt/package-name and sym links
* easy control of right, if another user needs access to that package just add him to group.
