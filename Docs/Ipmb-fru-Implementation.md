## Ipmb Based Multi-host Fru Read/Write Process

### Introduction

IPMB based host FRU has host board, chassis and product information.These
information follows standard IPMI format.

In Entity Manager, new daemon 'ipmb-fru-device' which is similar to
'fru-device' daemon would scan ipmb buses of all the hosts and read and write
all the host FRU details which is IPMB based interface.

### Required Repository

1. entity-manager
2. openbmc

### Implementation

The new "ipmb-fru-device" deamon is created for handling to read/write the FRU
details of all the hosts using ipmb interfaces. This deamon reads the ipmb
devices list from the Entity-manager platform specific config file.

- Sample Config :
   ```
        {
           "Name": "IpmbBus1",
           "Bus": "ipmb",
           "Index": 0,
           "Type": "IPMIChannels"
        },
        {
           "Name": "IpmbBus2",
           "Bus": "ipmb",
           "Index": 1,
           "Type": "IPMIChannels"
        }
   ```

Then scan all the ipmb devices and send ipmb commands to read the all the host
FRU details and create a dbus objects under
xyz.openbmc_project.Ipmb.FruDevice the dbus service.

Similarly, using ipmb commands can write the fru details for all the hosts.

If users want to use ipmb based fru to read the fru information, they just need
to add the ipmb bus details in entity-manager platform specific config file.
This will enable ipmb communication for the corresponding ipmi channel.
Also this will read/write the fru's info using ipmb-fru-device and create
dbus-objects.

Use case :

YosemiteV2 is multi host system. The BMC is connected with hosts with the ipmb
interface. The "ipmb-fru-device" deamon reads the ipmb channel list, scan the
ipmb busses, validate the FRU details and read/write the each host fru details.
Finally produces the dbus-objects for the host FRU's.
This configuration is based on the "xyz.openbmc_project.Ipmb.FruDevice"
service, which will read FRU information from each IPMB bus. "$bus"
will give the bus index for each IPMB channel.

### Gerrit Links

1. entity-manager   - https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/49418 <br/> 
                      https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/49205 <br/>
                      https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/49076 <br/>
                      https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/39592 <br/>
                      https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/47246 <br/> 
                      https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/50894 <br/>
                      https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/50921 <br/>
                      https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/51555 <br/>

2. openbmc          - https://gerrit.openbmc-project.xyz/c/openbmc/meta-phosphor/+/37513
