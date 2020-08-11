## Tiogapass Ethernet Interfaces
Procedure to get IP Addresses using redfish.
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
$ curl -k -H "X-Auth-Token: $token" -X GET https://${bmc}/redfish/v1/Managers/bmc/EthernetInterfaces/eth0
```

  - OUTPUT:
    ```
     {
 	 "@odata.id": "/redfish/v1/Managers/bmc/EthernetInterfaces/eth0",
	 "@odata.type": "#EthernetInterface.v1_4_1.EthernetInterface",
	 "DHCPv4": {
	    "DHCPEnabled": true,
 	    "UseDNSServers": true,
	    "UseDomainName": true,
	    "UseNTPServers": true
   	  },
	 "DHCPv6": {
	    "OperatingMode": "Stateful",
	    "UseDNSServers": true,
	    "UseDomainName": true,
	    "UseNTPServers": true
	  },
	 "Description": "Management Network Interface",
	 "FQDN": "tiogapass",
	 "HostName": "tiogapass",
	 "IPv4Addresses": [
	    {
	      "Address": "10.0.128.190",
	      "AddressOrigin": "DHCP",
	      "Gateway": "0.0.0.0",
	      "SubnetMask": "255.255.0.0"
	    },
	    {
	      "Address": "169.254.108.221",
	      "AddressOrigin": "IPv4LinkLocal",
	      "Gateway": "0.0.0.0",
	      "SubnetMask": "255.255.0.0"
	    }
	  ],
	  "IPv4StaticAddresses": [],
	  "IPv6AddressPolicyTable": [],
	  "IPv6Addresses": [
	    {
	      "Address": "fe80::9a03:9bff:fe86:c048",
	      "AddressOrigin": "LinkLocal",
	      "AddressState": null,
	      "PrefixLength": 64
	    }
	  ],
	  "IPv6DefaultGateway": "",
	  "IPv6StaticAddresses": [],
	  "Id": "eth0",
	  "InterfaceEnabled": true,
	  "LinkStatus": "LinkUp",
	  "MACAddress": "98:03:9b:86:c0:48",
	  "Name": "Manager Ethernet Interface",
	  "NameServers": [
	    "10.0.0.1"
	  ],
	  "SpeedMbps": 0,
	  "StaticNameServers": [],
	  "Status": {
	    "Health": "OK",
	    "HealthRollup": "OK",
	    "State": "Enabled"
	  },
	 
	}
       ```	
