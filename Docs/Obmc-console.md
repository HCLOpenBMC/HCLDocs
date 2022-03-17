## Added Obmc-console Support For Yosemitev2 Multi-host Platform

### Introduction

The obmc-console and obmc-console log support added for Facebook yosemiteV2
multi-host platform.

The server and client configurations files were added in openbmc meta-facebook
repo to add obmc-console and obmc-console log support in YosemiteV2 platform.

### Required Repository

1. openbmc

### Implementation

The obmc-console and obmc-console log support added for YosemiteV2 platform.

The Generic implementation of obmc-console is already added for obmc-console
repo for multi-host. 

The conf files like server.conf and client.conf needs to be configured
dynamically in platform specific machine layer in openbmc repo.

The server.conf has "socket-id", "baud", "tty" as the parameters.
socket-id shall be like "host0" for single hosts, "host0", "host1", "host2"
and "host3" for multi-host. buad shall be 56700 based on their platform baud rate.
tty shall ve ttyS0 to ttyS3.

The client.conf has "socket-id" as host0 to host3 for their respective server.conf
file. "socket-id" value should be same as in both server.conf and client.conf file.

obmc-console works based on client and server based socket communication.This
application enables the client and server socket communication for host console.
Now, host console will be enabled and can logged into host console.

Also, all the host console log can be stored in /var/log/obmc-console*.log paths.

### Gerrit Links

1. openbmc          - https://gerrit.openbmc-project.xyz/c/openbmc/meta-facebook/+/31318 <br/>
                      https://gerrit.openbmc-project.xyz/c/openbmc/meta-facebook/+/32182
