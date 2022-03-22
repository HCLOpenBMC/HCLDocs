## MULTI-HOST INFORMATION IS DISPLAYED IN THE OCP-DEBUG CARD

### INTRODUCTION

The following pieces of information are going to be displayed in the OCP Debug-Card
for all four hosts.

1. System Info

   The content of this system info frame contains pre-defined key information as below:
   * Serial Number
   * Part Number
   * BMC IP
   * BMC FW ver.
   * BIOS FW ver.
   * ME status
   * Board ID
   * Sys Conf.info:CPU/Mem/HDD etc.

2. Critical SEL

   The content of this critical sel frame contains all pre-defined BMC critical SELs.

3. Critical Sensor

   The content of this critical sensor frame contains all pre-defined BMC critical
   sensors.

##REQUIRED REPOSITORY

1. fb-ipmi-oem

### IMPLEMENTATION PROCESS

The existing implementation of host information displayed in the OCP Debug-card
will does not support for multi-host systems. it supports only for single-host
systems. So, now it's implemented for multi-host systems as well.

The Debug Card sends the IPMB request to BMC, and BMC responds to the brief
message back according to the request command.

Before going to display those pieces of information in OCP Debug-Card, the 
information needs to be collected from the host and stored in BMC. then
particular handler function will display the corresponding information
to the OCP Debug-Card.

### GERRIT LINKS

 fb-ipmi-oem 
 1. https://gerrit.openbmc-project.xyz/c/openbmc/fb-ipmi-oem/+/50439
 2. https://gerrit.openbmc-project.xyz/c/openbmc/fb-ipmi-oem/+/50440
