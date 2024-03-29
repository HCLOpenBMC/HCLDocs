## Added Support For Voltage, Temperature, Fansensor and Airflow Sensor Support

### Introduction

The Voltage sensors, Inlet, Outlet and NIC temperature sensors, Fansensors and
Airflow sensor support added for yosemiteV2 platform.

These sensor has to be configured dynamically using entity-manager platform
specific config file which is FBYV2.json. 

### Required Repository

1. entity-manager
2. openbmc

### Implementation

The Voltage sensors like ADC sensors, Inlet, Outlet and NIC temperature sensors
like TMP421 and Fansensors like AspeedFan support added for Facebook YosemiteV2
platform.

The Generic implementation of these sensors like ADC, Temperature and Fan sensors
are already added in entity-manager and dbus-sensors repository. Also firmware
driver support added for these sensors by configuring in the .dts file for the
specific platforms.

These sensors needs to be configured dynamically using entity-manager platform
specific config file. These sensors are directly connected to BMC. So Baseboard
FruDevice interface is added in "Probe" field in config file.

Then all the sensors are added with Name, Bus, Address, Thresholds etc. Mainly
"Type" field needs to be configured correctly. Based on this Type field, the
sensor validaion and operations handling in the dbus-sensors.

Entity-manger reads, parse the json files and probs the fru interface and scans
all the buses and vaildate all the configured sensors with sysfs nodes.
Then finally generates dbus-objects and dbus-interfaces for all the sensors
with all required properties.

- Sample Config :
   ```
       {
            "Index": 0,
            "Name": " SP_P5V",
            "ScaleFactor": 0.2782,
            "Thresholds": [
                {
                    "Direction": "greater than",
                    "Name": "upper critical",
                    "Severity": 1,
                    "Value": 5.5
                },
                {
                    "Direction": "less than",
                    "Name": "lower critical",
                    "Severity": 1,
                    "Value": 4.5
                }
            ],
            "Type": "ADC"
       },
       {
            "Address": "0x4f",
            "Bus": 9,
            "Name": "SP_OUTLET_TEMP",
            "Name1": "SP_OUTLET_REMOTE_TEMP",
            "Thresholds": [
                {
                    "Direction": "greater than",
                    "Name": "upper critical",
                    "Severity": 1,
                    "Value": 70
                }
            ],
            "Type": "TMP421"
        }
   ```

The full json FBYV2.json is given in the below gerrit link.

- Airflow Sensor :

  Airflow sensor is added as virtual sensor in yosemiteV2 platform. This
Airflow sensor support added in phosphor-virtual-sensor application with
generic implementation. 

  Airflow sensor value is calculated from both fans value in YosemiteV2. These
Fan values and Expression are configured in the platform specific config file
in machine later. Also, this phosphor-virtual-sensor application needs to be
enabled in the platform specific machine layer.

  Phosphor-virtual-sensor application reads and parse the json config file, then
reads the both Fan values given in the "Params" field in json. Based on the
expression formula, it does the calculation and find the Airflow sensor value.
Finally, dbus-objects and interfaces are created for this Airflow sensor.

### Gerrit Links

1. entity-manager   - https://gerrit.openbmc-project.xyz/c/openbmc/entity-manager/+/27221
2. openbmc          - https://gerrit.openbmc-project.xyz/c/openbmc/meta-facebook/+/28192 <br/>
                    - https://gerrit.openbmc-project.xyz/c/openbmc/meta-facebook/+/28211 <br/>
                    - https://gerrit.openbmc-project.xyz/c/openbmc/openbmc/+/40671
