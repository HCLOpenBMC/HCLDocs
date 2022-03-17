## Added Ipmi Implementation To Handle Bic Request

### Introduction

The Ipmi implementation to handle BIC request support added for Facebook
yosemiteV2 multi-host platform. It supports other Facebook platforms as well
which has Bridge-IC.

The new handler is registered and added for handling this BIC request with
IPMI netfn and IPMI cmd. 

### Required Repository

1. fb-ipmi-oem
2. openbmc

### Implementation

Ipmi Implementation to handle Bridge-Ic request support is added for YosemiteV2
platform.

The new handler is registered and added for handling this BIC request with
IPMI netfn and IPMI cmd. 

The IPMI command request are coming from Host to BMC. So this registered handler
gets called when the netfn as 0x38 and cmd as 0x1 coming from Host to BMC via
ipmbbridge. 

The handler function receives ctx, iana, interface, lun, netfn, cmd, data as
parameters and calls the internal another ipmi command execution function with
new ipmi command request. That command will call the another ipmi hanlder and
send the response back to requester. Because, this IPMI command  has another
IPMI command wrapped in it.

Example :
Ipmi command received in this handler function is 0x38 0 1 6 0x15 0xa0 0 3 6 1 0.
Another ipmi command 6 1 0 is wrapped in it. 

Now, all the IPMI commands coming from HOST to BMC via Birdge-IC is handled
using this handler.

### Gerrit Links

1. fb-ipmi-oem      - https://gerrit.openbmc-project.xyz/c/openbmc/fb-ipmi-oem/+/33493 <br/>
2. openbmc          - https://gerrit.openbmc-project.xyz/c/openbmc/meta-facebook/+/33692 
