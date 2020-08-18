## Tiogapass PostCode Logs
Procedure to get postcode logs using redfish.
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
$ curl -k -H "X-Auth-Token: $token" -X GET https://${bmc}/redfish/v1/Systems/system/LogServices/PostCodes/Entries
```
   - OUTPUT:
      ```
      {
	  "@odata.context": "/redfish/v1/$metadata#LogEntryCollection.LogEntryCollection",
	  "@odata.id": "/redfish/v1/Systems/system/LogServices/PostCodes/Entries",
	  "@odata.type": "#LogEntryCollection.LogEntryCollection",
	  "Description": "Collection of POST Code Log Entries",
	  "Members": [
	    {
	      "@odata.context": "/redfish/v1/$metadata#LogEntry.LogEntry",
	      "@odata.id": "/redfish/v1/Systems/system/LogServices/PostCodes/Entries/B1-1",
	      "@odata.type": "#LogEntry.v1_4_0.LogEntry",
	      "Created": "1970-01-01T00:01:02+00:00",
	      "EntryType": "Event",
	      "Id": "B1-1",
	      "Message": "Boot Count: 1: TS Offset: 0.0000; POST Code: 0x06",
	      "MessageArgs": [
	        "1",
	        "0.0000",
	        "0x06"
	      ],
	      "MessageId": "OpenBMC.0.1.BIOSPOSTCode",
	      "Name": "POST Code Log Entry",
	      "Severity": "OK"
	    },
	  ...
     	  ],
	  "Members@odata.count": 16,
	  "Members@odata.nextLink": "/redfish/v1/Systems/system/LogServices/PostCodes/Entries?$skip=1000",
	  "Name": "BIOS POST Code Log Entries"
      }
      ```

