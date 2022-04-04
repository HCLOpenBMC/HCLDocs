## Support for sync bmc time from host time via IPMB

### Introduction

    The BMC does not have the RTC and have only way of updating the time via
Network. In case if the NTP is not active then bmc time cannot be updated.
If NTP is not active then this feature adds support to poll the host time via
 ipmi commands and sets the bmc time got from the host.

### Required Repository

1. openbmc

### Implementation

    This change is done as shell script which is started as one time systemd
service at bmc startup.the script is part of machine layer.When the script
 starts,first the NTP status is checked. If the NTP is not active then the
 host time is requested via ipmi.

    If the bmc system is single host the host time is requested via IPMI and
 then received host time is set is BMC time if the response is success.

    For the multi host system each host is polled for the time via IPMB
commands and the time of the host with successful response is then set as the
 BMC time.

### Gerrit Links

1. openbmc     - https://gerrit.openbmc-project.xyz/c/openbmc/openbmc/+/47614
