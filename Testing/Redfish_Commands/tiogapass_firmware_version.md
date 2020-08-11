## Tiogapass Firmware Version
Procedure to read firmware version using redfish.
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
To read BMC Version
```
$ curl -k -H "X-Auth-Token: $token" -X POST https://${bmc}/redfish/v1/UpdateService/FirmwareInventory/<image_id>
```
   - OUTPUT:
      ```
      {
	  "@odata.id": "/redfish/v1/UpdateService/FirmwareInventory/a77348be",
	  "@odata.type": "#SoftwareInventory.v1_1_0.SoftwareInventory",
	  "Description": "BMC image",
	  "Id": "a77348be",
	  "Members@odata.count": 1,
	  "Name": "Software Inventory",
	  "RelatedItem": [
	    {
	      "@odata.id": "/redfish/v1/Managers/bmc"
	    }
	  ],
	  "Status": {
	    "Health": "OK",
	    "HealthRollup": "OK",
	    "State": "Enabled"
	  },
	  "Updateable": true,
	  "Version": "2.9.0-dev-200-g8f3c9bb74"
      }
      ```

### STEP - 4
To read ME Version
```
$ curl -k -H "X-Auth-Token: $token" -X POST https://${bmc}/redfish/v1/UpdateService/FirmwareInventory/me
```
   - OUTPUT:
      ```
      {
	  "@odata.id": "/redfish/v1/UpdateService/FirmwareInventory/me",
	  "@odata.type": "#SoftwareInventory.v1_1_0.SoftwareInventory",
	  "Description": "ME image",
	  "Id": "me",
	  "Name": "Software Inventory",
	  "Status": {
	    "Health": "OK",
	    "HealthRollup": "OK",
	    "State": "Enabled"
	  },
	  "Updateable": false,
	  "Version": "4.0.4.393.0"
      }
      ```
