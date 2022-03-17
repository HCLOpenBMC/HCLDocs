## Added Hostlogger Support For Yosemitev2 Multi-host Platform

### Introduction

The Hostlogger support added for Facebook yosemiteV2 multi-host platform.

The configurations files were added in openbmc meta-facebook repo to add
hostlogger support in YosemiteV2 platform.

### Required Repository

1. openbmc

### Implementation

The Hostlogger support added for YosemiteV2 platform to store console log
histories for all the host.

The Generic implementation of Hostlogger is already added for
phosphor-hostlogger repo for multi-host. So, this features needs to enabled
in platform specific machine layer with configuration files for single-host
and as well as multi-host systems.

The conf files like ttyS0.conf, ttyS1.conf, etc ., needs to be configured
dynamically in platform specific machine layer in openbmc repo.

The ttyS[0-3].conf has "socket-id", "Buf-MaxSize", "host_state" and "out-dir"
as the parameters. socket-id shall be like "host0" for single hosts, "host0",
"host1", "host2" and "host3" for multi-host. Buf-MaxSize shall be 3000,
host_state shall be /xyz/openbmc_project/state/host[1-4] and out-dir shall be 
/var/lib/obmc/hostlogs/host[1-4]. The all the host console log histories can be
stored in the out-dir path.

phosphor-hostlogger works based on configuration files based on the
communication with obmc-console to get the console information and store all
the console log histories in the out-dir which is configured in .conf files.

### Gerrit Links

1. openbmc          - https://gerrit.openbmc-project.xyz/c/openbmc/openbmc/+/40667
