## Perforce / Helix Guide for UE4 on a linux server

This guides explain how to set up a Perforce/Helix P4 server to host your [UE4](https://www.unrealengine.com/) project on it.

This guides uses Ubuntu 18.04.

### Prerequisites

You should have your Linux server already set up and be able to connect to it via SSH. Connect as root to your server:

`ssh -lroot IPADRESS`

### Getting started

This guide uses Ubuntu 18.04, but it should work on other Linux distributions as well. We are going to use the Linux package-based installation for this guide. Two distribution packages can be used Debian (.deb) for Ubuntu systems and RPM (.rpm) for CentOS, RedHat and SUSE. Make sure to install the correct package.

Available Perforce packages for Linux (Intel x86_64) platforms are:

- Ubuntu 12.04 LTS (precise)
- Ubuntu 14.04 LTS (trusty)
- Ubuntu 16.04 LTS (xenial)
- Ubuntu 18.04 LTS (bionic)
- CentOS or Red Hat 6.x
- CentOS or Red Hat 7.x
- SUSE Linux Enterprise Server 12

Given that list, we are using the "bionic" release.

### Installation

1. Add the Perforce packaging key to your APT keyring

`wget -qO - https://package.perforce.com/perforce.pubkey | sudo apt-key add -`

Server should respond with "OK".

2. Add the Perforce repository to your APT configuration.

To do this, change directory to "/etc/apt/sources.list.d/":

`cd /etc/apt/sources.list.d/`

Now create a file named "perforce.list", e.g. with VIM:

`vim perforce.list`

and enter the following (press "I" on your keyboard to start writing):

`deb http://package.perforce.com/apt/ubuntu bionic release`

press ESC to enter comamnd mode and type ":wq" to save and quit. *NOTE*: We used "bionic" since we are using Ubuntu 18.04. If you are using another version, make sure to replace it with the appropriate distribution (see Getting Started).

3. Run `apt-get update` to download the necessary packages. The output should look somewhat like this:

```
Hit:1 http://asi-fs-n.contabo.net/ubuntu bionic InRelease
Hit:2 http://asi-fs-n.contabo.net/ubuntu bionic-updates InRelease
Hit:3 http://asi-fs-n.contabo.net/ubuntu bionic-backports InRelease
Hit:4 http://security.ubuntu.com/ubuntu bionic-security InRelease
Get:5 http://package.perforce.com/apt/ubuntu bionic InRelease [3,411 B]
Get:6 http://package.perforce.com/apt/ubuntu bionic/release amd64 Packages [3,582 B]
```

4. Run `sudo apt-get install helix-p4d` to start the installation. After a successfull installation the output should look like this:

```
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
::
::  Thank you for choosing Perforce Helix
::  The following has been installed by the 'helix-p4d' package:
::
::  - The Helix Version Engine (p4d)
::  - A 'perforce' system user
::  - p4dctl, a tool for managing Perforce service instances
::  - The Helix Command-Line Client (p4)
::
::  The Helix Version Engine is now installed, but not yet configured.
::  You must run the following to configure p4d (as root):
::
::    sudo /opt/perforce/sbin/configure-helix-p4d.sh
::
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Started 0 services.
No services configured.
```

Perforce / Helix P4 is now installed. As stated in the output, the service isn't running yet. Helix needs to be configurated first.

### Configuration

1. Start the configuration in Interactive Mode by running:

`sudo /opt/perforce/sbin/configure-helix-p4d.sh`

The following options can be configured to ones liking, using the default values is fine, too. At the end of the configuration mode you will be asked to create a user and a password for the super user.

The setup is now complete and a summary of the configuration options will be displayed. You should now be able to connect to your P4 server via P4V.
