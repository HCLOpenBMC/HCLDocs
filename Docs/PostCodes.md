## Added Postcode Support for multi-host platforms.

### Introduction

The Earlier version of OpenBMC does not support postcodes for multi-host
systems. It supports only for single-host systems. So, Proposed the design to
support postcodes for multi-host system. Implementation done for added postcode
support in Facebook YosemiteV2 platform as well.

The both phosphor-postcode-manager and phosphor-host-postd applications updated
to handle this postcode support for multi-host system. 

### Required Repository

1. phosphor-postcode-manager
2. phosphor-host-postd
3. fb-ipmi-oem
3. openbmc

### Implementation

Please refer the below gerrit link for this design and implementation of this feature.
https://gerrit.openbmc-project.xyz/c/openbmc/docs/+/35065 

### Gerrit Links

1. phosphor-postcode-manager - https://gerrit.openbmc-project.xyz/c/openbmc/phosphor-post-code-manager/+/36145
2. fb-ipmi-oem               - https://gerrit.openbmc-project.xyz/c/openbmc/fb-ipmi-oem/+/36112
3. phosphor-host-postd       - https://gerrit.openbmc-project.xyz/c/openbmc/phosphor-host-postd/+/45805
4. openbmc                   - https://gerrit.openbmc-project.xyz/c/openbmc/meta-phosphor/+/36148<br/>
                               https://gerrit.openbmc-project.xyz/c/openbmc/meta-facebook/+/36147<br/>
                               https://gerrit.openbmc-project.xyz/c/openbmc/openbmc/+/45988<br/>
                               https://gerrit.openbmc-project.xyz/c/openbmc/openbmc/+/45810<br/>
