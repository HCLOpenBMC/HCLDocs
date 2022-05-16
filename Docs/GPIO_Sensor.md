### IPMB BASED GPIO STATE SENSOR

## INTRODUCTION

Gpio is a dbus property represents the ON/OFF state of the host's
gpio.
The support is added to get the ipmb gpio states via ipmb commands,
which is connected through IPMB.

## REQUIRED REPOSITORY

 1.dbus-sensors
 2.entity-manager

## IMPLEMENTATION PROCESS

Currently the direct GPIO states can be read for the single host.
In this implementation, the GPIO state for the multi-host is
introduced as a Dbus interface via ipmbbridge.
```
       {
            "Address": "0x03",
            "Bus": "$bus",
            "Class": "twin_lake_gpio",
            "Name": "$bus + 1 CPU Good",
            "SensorType": "ipmbGpioState",
            "Type": "TwinlakeHostController"
        }
```
This configuration is based on the "xyz.openbmc_project.Ipmb.FruDevice"
service, which will read FRU information from each IPMB bus."$bus" will
give the bus index for each IPMB channel.If IPMB FRU is detected,
The host's for GPIO in each bus will be identified.

Then the IPMB command will be send, the response for each host 
will be received from that the GPIO state's like CPU Good,PCH Good,
bios state can be parshed.

Once the information is retrieved for the GPIO states,
dbus objects will be populated for each GPIO's. Finally, it will
read the specific GPIO state value from each host via IPMB and the
values will be updated in dbus property.

## GERRIT LINKS

https://gerrit.openbmc-project.xyz/c/openbmc/dbus-sensors/+/47952
https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/48005

