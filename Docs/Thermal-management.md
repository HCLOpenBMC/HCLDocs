## Thermal Management - Power off slots if FAN and NIC sensor values crosses thresholds.

### Introduction

FanSensors SP_FAN0_TACH and SP_FAN1_TACH values comes below the threshold level
of 500 and NIC sensor MEZZ_SENSOR values crosses above the theshold level of
120. In the both cases, all the slot would be powered off in Facebook
YosemiteV2 to reduce the temperature level in the system and also cool down
the heates components in the system.

"Severity" field values to be configured in platform specific config in
entity-manager for the Fan and NIC sensor. Based on the Severity level the
Warning, Critical and Hard/Soft Shutdwon dbus interfaces are created under Fan
and NIC sensor.

### Required Repository

1. entity-manager
2. dbus-sensors
3. phosphor-fan-presence
4. openbmc

### Implementation

The "Severity" field value is configured between 0 to 5. The below values are
configured for the corresponding interfaces to be created for Fan and NIC
sensors with High/Low properties and Alarms.

```
    Warning          - 0
    Critical         - 1
    Performance Loss - 2
    Soft Shutdown    - 3
    Hard Shutdown    - 4

```
 - Sample Config :
   ```
     {
            "Address": "0x1f",
            "Bus": 11,
            "Name": "MEZZ_SENSOR_REMOTE_TEMP",
            "Name1": "MEZZ_SENSOR_TEMP",
            "Thresholds": [
                {
                    "Direction": "greater than",
                    "Name": "upper critical",
                    "Severity": 1,
                    "Value": 105
                },
                {
                    "Direction": "greater than",
                    "Name": "upper non critical",
                    "Severity": 0,
                    "Value": 95
                },
                {
                    "Direction": "greater than",
                    "Name": "upper non recoverable",
                    "Severity": 4,
                    "Value": 120
                }
            ],
            "Type": "TMP421"
      }

   ```

If any of Fan sensors SP_FAN0_TACH or SP_FAN1_TACH values are comes below the
treshold level of 500, then based on the Severity level the shutdown alarms are
triggered. 

Similary, If NIC sensor MEZZ_SENSOR value goes above the threshold level of 120,
then based on the Severity level the shutdown alarms are triggered.

Severity value as 4 for Facebook YosemiteV2 platform to trigger the Hard shutdown
the slots. 

In phosphor-fan-presence, sensor-monitor application does the Sensor interfaces
monitoring, Alarm triggering and executing Hard/Soft Shutdown services and
script. It shutdowns all the four slots in YosemiteV2 platforms.

### Gerrit Links

1. entity-manager        - https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/50356<br/>
                           https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/50357 

2. dbus-sensors          - https://gerrit.openbmc-project.xyz/c/openbmc/dbus-sensors/+/49408<br/>
                           https://gerrit.openbmc-project.xyz/c/openbmc/dbus-sensors/+/49538<br/>
                           https://gerrit.openbmc-project.xyz/c/openbmc/dbus-sensors/+/50289<br/>

3. phosphor-fan-presence - https://gerrit.openbmc-project.xyz/c/openbmc/phosphor-fan-presence/+/49079

4. openbmc               - https://gerrit.openbmc-project.xyz/c/openbmc/openbmc/+/49107 
