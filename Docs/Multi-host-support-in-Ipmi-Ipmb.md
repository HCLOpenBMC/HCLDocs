## Added Multi-host Support in Ipmid and Ipmbridged.

### Introduction

The Earlier version of OpenBMC does not support multi-host implementation in
IPMI commands handling. Proposed the design to support multi-host system in
Ipmi and ipmbbridge commands handling.

The both ipmid and ipmbbridged applications updated to handle this Ipmi commands
handling for multi-host system. 

### Required Repository

1. phosphor-ipmi-host
2. ipmbbridge
3. openbmc

### Implementation

Plesae refer the below gerrit link for this design and implementation of this feature.
https://gerrit.openbmc-project.xyz/c/openbmc/docs/+/34464 

### Gerrit Links

1. phosphor-ipmi-host - https://gerrit.openbmc-project.xyz/c/openbmc/phosphor-host-ipmid/+/35781
2. ipmbbridge         - https://gerrit.openbmc-project.xyz/c/openbmc/ipmbbridge/+/34579 <br/>
                        https://gerrit.openbmc-project.xyz/c/openbmc/ipmbbridge/+/35782
3. openbmc            - https://gerrit.openbmc-project.xyz/c/openbmc/meta-facebook/+/34581
