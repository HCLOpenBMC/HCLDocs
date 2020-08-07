## Tiogapass BMC Image Update
Procedure to update image in BMC using redfish.
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
Update the BMC image using the below command.
```
$ curl -k -H "X-Auth-Token: $token" -X POST -T <image_path> https://${bmc}/redfish/v1/UpdateService
```
    - OUTPUT:
      ```
      {
       "@odata.id": "/redfish/v1/TaskService/Tasks/0",
       "@odata.type": "#Task.v1_4_3.Task",
       "Id": "0",
       "TaskState": "Running",
       "TaskStatus": "OK"
      }  
       ```
### STEP - 4
Reboot the BMC.
```
$ curl -k -H "X-Auth-Token: $token"  -X POST https://${bmc}/redfish/v1/Managers/bmc/Actions/Manager.Reset -d '{"ResetType":"GracefulRestart"}'
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
