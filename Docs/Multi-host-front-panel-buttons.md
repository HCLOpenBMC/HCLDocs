## multi host front panel support in phosphor-buttons.

### Introduction

This feature adds support for multi host front panel buttons.
The original phosphor buttons repo has support for single host frontpanel
button interfaces like power button and reset button.This feature adds
support for additional form factor type such as host selector,OCP debug
card host selector button which enables multiple host power and reset button
event handling.

### Required Repository

1. phosphor-buttons
2. phosphor-dbus-interfaces

### Implementation

The design and implementation details are given below :
https://gerrit.openbmc-project.xyz/c/openbmc/docs/+/45544
https://github.com/openbmc/docs/blob/master/designs/multihost-phosphor-buttons.md

### Gerrit Links

1. Add group gpio changes - https://gerrit.openbmc-project.xyz/c/openbmc/phosphor-buttons/+/49311
2. Add abstract factory to create button iface objects
         - https://gerrit.openbmc-project.xyz/c/openbmc/phosphor-buttons/+/49714

3. Add host selector interface - https://gerrit.openbmc-project.xyz/c/openbmc/phosphor-buttons/+/51183