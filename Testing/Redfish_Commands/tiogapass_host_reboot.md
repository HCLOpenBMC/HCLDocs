## Tiogapass Host Reboot
Procedure to reboot host using redfish.
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
$ curl -k -H "X-Auth-Token: $token" -X POST https://${bmc}/redfish/v1/Systems/system/Actions/ComputerSystem.Reset -d '{"ResetType": "ForceRestart"}'
```
   - OUTPUT:
      ```
      "@Message.ExtendedInfo": [
       {
         "@odata.type": "#Message.v1_0_0.Message",
         "Message": "Successfully Completed Request",
         "MessageArgs": [],
         "MessageId": "Base.1.4.0.Success",
         "Resolution": "None",
         "Severity": "OK"
       }
       ]
       ```
