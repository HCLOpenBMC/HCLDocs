## Tiogapass Sensors
Procedure to get sensors value using redfish.
(Using CURL commands)

### STEP - 1
Export the BMC IP Address in the terminal.
```
$ export bmc=xx.xx.xx.xx
```
### STEP - 2
Establish Redfish connection session with BMC using the below command.
```
$ export token=`curl -k -H "Content-Type: application/json" -X POST https://${bmc}/login -d '{"username" :  "root", "password" :  "0penBmc"}' | grep token | awk '{print $2;}' | tr -d '"'`
```
### STEP - 3
```
$ curl -k -H "X-Auth-Token: $token"  -X GET https://${bmc}/redfish/v1/Chassis/TiogaPass_Baseboard/Sensors
$ curl -k -H "X-Auth-Token: $token"  -X GET https://${bmc}/redfish/v1/Chassis/TiogaPass_Baseboard/Power
$ curl -k -H "X-Auth-Token: $token"  -X GET https://${bmc}/redfish/v1/Chassis/TiogaPass_Baseboard/Thermal
```

    - OUTPUT:
      ```
      "@odata.id": "/redfish/v1/Chassis/TiogaPass_Baseboard/Thermal",
      "@odata.type": "#Thermal.v1_4_0.Thermal",
      "Fans": [
      {
      "@odata.id": "/redfish/v1/Chassis/TiogaPass_Baseboard/Thermal#/Fans/0",
      "@odata.type": "#Thermal.v1_3_0.Fan",
      "LowerThresholdCritical": 500,
      "MaxReadingRange": 25000,
      "MemberId": "MB_FAN0_TACH",
      "MinReadingRange": 0,
      "Name": "MB FAN0 TACH",
      "Reading": 9178,
      "ReadingUnits": "RPM",
      "Status": {
        "Health": "Warning",
        "State": "Enabled"
      },
      "UpperThresholdCritical": 11500,
      "UpperThresholdNonCritical": 8500
      }
      ]

      "Temperatures": [
      {
      "@odata.id": "/redfish/v1/Chassis/TiogaPass_Baseboard/Thermal#/Temperatures/0",
      "@odata.type": "#Thermal.v1_3_0.Temperature",
      "MaxReadingRangeTemp": 127.0,
      "MemberId": "Core_1_CPU1",
      "MinReadingRangeTemp": -128.0,
      "Name": "Core 1 CPU1",
      "ReadingCelsius": 25.0,
      "Status": {
        "Health": "OK",
        "State": "Enabled"
      },
      "UpperThresholdCritical": 93.0,
      "UpperThresholdNonCritical": 83.0
      }
      ]

      "Voltages": [
      {
      "@odata.id": "/redfish/v1/Chassis/TiogaPass_Baseboard/Power#/Voltages/0",
      "@odata.type": "#Power.v1_0_0.Voltage",
      "LowerThresholdCritical": 10.77,
      "MaxReadingRange": 20.0,
      "MemberId": "_MB_P12V",
      "MinReadingRange": 0.0,
      "Name": " MB P12V",
      "ReadingVolts": 12.331,
      "Status": {
        "Health": "OK",
        "State": "Enabled"
      },
      "UpperThresholdCritical": 13.23
      }
      ]
      ```

