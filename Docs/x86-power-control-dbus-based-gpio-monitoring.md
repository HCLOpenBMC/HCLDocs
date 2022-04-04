## Monitoring of power control GPIO line states via DBUS interface.

### Introduction

The x86-power-control monitors the direct gpio line changes. In some cases the
power state gpio lines such as pgood cannot be a direct gpio line and needs to
 be accessed as other means such as ipmi interface. For the gpio lines that
 can be accessed as direct gpio, dbus based gpio monitoring support is added
 in x86 power control.

### Required Repository

1. openbmc
2. x86-power-control

### Implementation

This is done by introducing a new type of gpio config(dbus gpio config) apart from
already existing direct gpio config.

The direct gpio config has the following format :
```
{
    "Name" : "PostComplete",
    "LineName" : "POST_COMPLETE",
    "Type" : "GPIO"
}
```

The dbus based gpio config has the following format :
```
{
    "Name" : "PowerButton",
    "DbusName" : "xyz.openbmc_project.Chassis.Event",
    "Path" : "/xyz/openbmc_project/Chassis/Event",
    "Interface" : "xyz.openbmc_project.Chassis.Event",
    "Property" : "PowerButton_Host1",
    "Type" : "DBUS"
}
```
when the x86 power control prepares for setup event handlers for the gpio
 line, based on the gpio config type It sets up the respective event handlers.

i.e for direct dpio it uses the event handler based on libgpiod
and for dbus gpio config sdbusplus match is setup as event handler.

Note : This feature expects that separate process which updates
the gpio state chages on the respective dbus interface for every
dbus GPIO config mentioned.

### Gerrit Links

1. openbmc                   - https://gerrit.openbmc-project.xyz/c/openbmc/x86-power-control/+/48779
                                https://gerrit.openbmc-project.xyz/c/openbmc/openbmc/+/48807
2. x86-power-control         - https://gerrit.openbmc-project.xyz/c/openbmc/x86-power-control/+/36528

