##IPMB BASED SDR SENSOR

###INTRODUCTION

SDR is a data record that provides platform management sensor type,
locations, event generation and access information.

A data records that contain information about the type and the
number of sensors in the platform, sensor threshold support,
event generation capabilities and information on what type
of readings the sensor provides.

###REQUIRED REPOSITORY

1. dbus-sensors
2. entity-manager

###IMPLEMENTATION PROCESS

Here, SDR of Type 1 records are implemented based on IPMB to read
the sensor information from each bus which can be configured
using IPMB FRU from the EM file.

- Sample Config :
   ```
   {
       "Name": "$bus + 1 SDR",
       "Bus": "$bus",
       "Class": "IpmbSDR",
       "PowerState": "Always",
       "Type": "SDRSensor"
   }
   ```

This configuration is based on the "xyz.openbmc_project.Ipmb.FruDevice"
service, which will read FRU information from each IPMB bus. "$bus"
will give the bus index for each IPMB channel.

If IPMB FRU is detected, SDR info and record count of the sensor in
each bus will be identified. After getting the record count,
Reservation ID for each IPMB bus will be received.

Then, data packet will be framed based on reservation ID to get the
full information of each sensor like sensor name, sensor type,
sensor unit, threshold values, sensor unique number using IPMB.

Once the information is retrieved for all the sensor based on record
count, dbus objects will be populated for each sensor. Finally, it
will read the sensor value from sensor unique number and the values
will be updated in dbus property.

