## Multi host x86 power control support

## Introduction
The earlier version of x86-power-control was only supported single host
based power control.
This multi host x86-power-control introduced power control support for
multihost systems. This change is achieved by running separate instance of
power control for each host with separate dbus name.

## Required Repository
1. openbmc
2. x86-power-control

## Implementation

    The multi host x86-power-control is achieved creating multiple
instances of x86 power control process w.r.t the number of host instances.
The multiple instance of x86 power control is achieved by creating systemd
service files.As a first step, the number of host instances is derived from
the yocto build variable OBMC_HOST_INSTANCES.

    Then based on the host instances number the x86-power-control systemd
 service files are created. The host number is passed as argument to the main
 from the each systemd service file. Each instance of the x86 power control
  will have the following  power state dbus names appended with the host number.

```
Single host power state dbus names :
Host dbus name : xyz.openbmc_project.State.Host
Chassis dbus name : xyz.openbmc_project.State.Chassis
OS dbus name : xyz.openbmc_project.State.OperatingSystem
Button DbusName : xyz.openbmc_project.Chassis.Buttons
NMI Dbus Name : xyz.openbmc_project.Control.Host.NMI
Restart Cause Dbus Name : xyz.openbmc_project.Control.Host.RestartCause
```
As an example consider a multi host system with four hosts,
four instances of power control will be created and the host
dbus names for four hosts will be as given below.

Multi host power state dbus names for host name :
```
 xyz.openbmc_project.State.Host1
 xyz.openbmc_project.State.Host2
 xyz.openbmc_project.State.Host3
 xyz.openbmc_project.State.Host4

```
### GPIO lines json config
For single host x86-power-control there was one json config file which has the
 associated GPIO line configs.
For the multi host x86 power control each host should have separate json cofig
file  created and respective GPIO line config should be provided for all config
files. These json config files shall be provided in the machine layer.


### Gerrit Links

1. x86-power-control          - https://gerrit.openbmc-project.xyz/c/openbmc/x86-power-control/+/43545
                                https://gerrit.openbmc-project.xyz/c/openbmc/x86-power-control/+/36528
2. openbmc                    - https://gerrit.openbmc-project.xyz/c/openbmc/x86-power-control/+/48779
                                https://gerrit.openbmc-project.xyz/c/openbmc/openbmc/+/48807