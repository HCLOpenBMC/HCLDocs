## BOOT ORDER CONFIGURATION

### INTRODUCTION

Boot order configuration will be used to set parameters that direct
the system boot following a system power up and to retrieve the boot
options. System BIOS will read these settings from the BMC and update
the boot order.

### REQUIRED REPOSITORY

1. fb-ipmi-oem
2. openbmc

### IMPLEMENTATION PROCESS

A yaml file is added in machine layer to create boot order interfaces
and property with default value based on number of host. Also the number
of host instances for a platform is passed to fb-ipmi-oem repo.

While host is booting, it will communicate with BMC to read the boot order configuration.
BMC will read ctx->hostIdx from host to confirm the host ID and compare it with the 
host instances which is read from bb file.

Once the host ID is verified, boot order information will be fetched from the respective 
dbus objects if it is already present or it will send the default boot order to set the
system BIOS.

### GERRIT LINKS

1. fb-ipmi-oem - https://gerrit.openbmc-project.xyz/c/openbmc/fb-ipmi-oem/+/38614
2. openbmc     - https://gerrit.openbmc-project.xyz/c/openbmc/openbmc/+/40285
