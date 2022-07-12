# Channels and Units of Sensors

<img src="../../img/dw_fc_snr.png" width="300px" />

The table below shows which channels can be accessed by each sensor using the `get_channel_data()` function

|Sensor name            |Channel Name                    |
|-----------------------|--------------------------------|
|all                    |timestamps, unaltered_timestamps|
|audio                  |microphone                      |
|compressed audio       |compressed_audio, audio_codec   |
|image                  |image, image_codec              |
|pressure               |pressure                        |
|light                  |light                           |
|proximity              |proximity                       |
|ambient temperature    |ambient_temp                    |
|relative humidity      |rel_humidity                    |
|accelerometer          |accelerometer_x, accelerometer_y, accelerometer_z|
|magnetometer           |magnetometer_x, magnetometer_y, magnetometer_z|
|linear acceleration    |linear_accel_x, linear_accel_y, linear_accel_z|
|orientation            |orientation_x, orientation_y, orientation_z|
|rotation vector        |rotation_vector_x, rotation_vector_y, rotation_vector_z|
|gyroscope              |gyroscope_x, gyroscope_y, gyroscope_z|
|gravity                |gravity_x, gravity_y, gravity_z |
|location, best location|gps_timestamps, latitude, longitude, altitude, speed, bearing, horizontal_accuracy, vertical_accuracy, speed_accuracy, bearing_accuracy, location_provider|
|station health         |battery_charge_remaining, battery_current_strength, internal_temp_c, network_type, network_strength, power_state, avail_ram, avail_disk, cell_service, cpu_utilization, wifi_wake_lock, screen_state, screen_brightness|

For more details on accessing the values from specific types of sensors, please read 
[Sensor Subclasses](https://github.com/RedVoxInc/redvox-python-sdk/tree/master/docs/python_sdk/data_window/station#sensor-subclass-functions).

The table below lists the sensors and their data's units

|Sensor name             |Channel Name            |units of data|
|------------------------|------------------------|-------------|
|all                     |timestamps, unaltered_timestamps|microseconds since epoch UTC|
|accelerometer           |                        |meters/second^2|
|ambient temperature     |                        |degrees Celsius|
|audio                   |                        |normalized counts (normalization constant = 0x7FFFFF)|
|compressed audio        |                        |bytes (codec specific)|
|gravity                 |                        |meters/second^2|
|gyroscope               |                        |radians/second|
|image                   |                        |bytes (codec specific)|
|light                   |                        |lux|
|linear acceleration     |                        |meters/second^2|
|magnetometer            |                        |microtesla|
|orientation             |                        |radians|
|pressure                |                        |kilopascal (this is also known as barometer sensor)|
|proximity               |                        |cm (this is also known as infrared sensor)|
|relative humidity       |                        |percentage|
|rotation vector         |                        |Unitless|
|location, best location |gps_timestamps          |microseconds since epoch UTC|
|                        |latitude, longitude, bearing, bearing accuracy|degrees| 
|                        |altitude, horizontal accuracy, vertical accuracy|meters|
|                        |speed, speed_accuracy   |meters per second|
|                        |location_provider       |enumeration of LocationProvider|
|station health          |battery_charge_remaining, cpu_utilization, screen_brightness|percentage|
|                        |battery_current_strength|microamperes|
|                        |internal_temp_c         |degrees Celsius|
|                        |network_type            |enumeration of NetworkType|
|                        |network_strength        |decibel|
|                        |power_state             |enumeration of PowerState|
|                        |avail_ram, avail_disk   |bytes|
|                        |cell_service            |enumeration of CellServiceState|
|                        |wifi_wake_lock          |enumeration of WifiWakeLock|
|                        |screen_state            |enumeration of ScreenState|

If Channel Name is blank, then all non-timestamp channels in the table have the unit specified.

Refer to the previous table for specific channel names for each sensor.

It is intentional that location and best location sensors share the same channel names.