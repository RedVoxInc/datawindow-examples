# Accessing Sensors in a Station

![](../img/dw_fc_snr.png)

In this example we will access the Sensor data in a Station.

## What is Sensor

A Sensor is a single device that records data.  Examples of a sensor would be a microphone, barometer and accelerometer.
Sensors in Stations are identified by their sensor type.

## Getting Sensor from Station

This example shows how to access the Sensor data in the Station.

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# get the first station
stn = dw.first_station()

# get all the data as a list of Sensors
data = stn.data()

# iterate over the sensors
for d in data:
    print(d.name)

# get a list of sensor types
types = stn.get_station_sensor_types()
```

Use the types listed by the function to get the corresponding Sensors.  If the return value of a function is 
`None`, the Sensor doesn't exist for that Station.

Here is an example of getting commonly used Sensors.

```python
from redvox.common.data_window import DataWindow
from redvox.common.sensor_data import SensorType

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# get the first station
stn = dw.first_station()

# Change the value in the line below to be the type you want to get
target_type = SensorType.AUDIO
# get a sensor of a specific type
sensor = stn.get_sensor_by_type(target_type)

# get the audio sensor
audio = stn.audio_sensor()

# get the barometer sensor
baro = stn.barometer_sensor()

# get the accelerometer sensor
accel = stn.accelerometer_sensor()

# get the gyroscope sensor
gyro = stn.gyroscope_sensor()

# get the magnetometer sensor
mag = stn.magnetometer_sensor()

# get the health sensor
hlth = stn.health_sensor()

# get the location sensor
loc = stn.location_sensor()
```

## Sensor Metadata

Every Sensor also has metadata that provides a high-level description of it.  One metadata value is required for a 
Sensor to exist: `name`.

Here is an example of accessing Sensor metadata:

```python
from redvox.common.sensor_data import SensorData

sen = SensorData("test_sensor")

# Print the sensor's name
print(sen.name)

# Print the sensor's type
print(sen.type())

# Print the sensor's type as a string
print(sen.type_as_str())

# Print the sensor's mean sample rate in hz
print(sen.sample_rate_hz())

# Print the sensor's mean sample interval in seconds
print(sen.sample_interval_s())

# Print the sensor's sample interval's standard deviation in seconds
print(sen.sample_interval_std_s())

# Print whether the sensor's sample rate is a constant value
print(sen.is_sample_rate_fixed())

# Print the sensor's metadata
print(sen)
```

## Sensor Data

Sensor data is stored in structures we call channels.  Accessing the data of the Sensor requires slightly different 
functions depending on the type of the Sensor.

Refer to the documentation on [Sensor Subclass](https://github.com/RedVoxInc/redvox-python-sdk/tree/master/docs/python_sdk/data_window/station#sensor-subclass-functions)
for more information about these functions.

All Sensors have timestamps, which are in [UTC](https://www.timeanddate.com/time/aboututc.html).

This example shows how to access the timestamps of a Sensor:

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# get the first station
stn = dw.first_station()

# get from a specific sensor
audio = stn.audio_sensor()
audio_timestamps = audio.data_timestamps()

# get from all sensors
sensors = stn.get_station_sensor_types()
for s in sensors:
    timestamps = stn.get_sensor_by_type(s).data_timestamps()
```

Refer to this [table](04a_sensor_units.md#units-of-the-data) for more information on the units of the data.

This example shows how to access data from commonly used sensors:

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# get the first station
stn = dw.first_station()

# get the audio sensor
audio = stn.audio_sensor()
data = audio.get_microphone_data()

# get the barometer (pressure) sensor
baro = stn.barometer_sensor()
data = baro.get_pressure_data()

# get the accelerometer sensor
accel = stn.accelerometer_sensor()
data_x = accel.get_accelerometer_x_data()
data_y = accel.get_accelerometer_y_data()
data_z = accel.get_accelerometer_z_data()

# get the gyroscope sensor
gyro = stn.gyroscope_sensor()
data_x = gyro.get_gyroscope_x_data()
data_y = gyro.get_gyroscope_y_data()
data_z = gyro.get_gyroscope_z_data()

# get the magnetometer sensor
mag = stn.magnetometer_sensor()
data_x = mag.get_magnetometer_x_data()
data_y = mag.get_magnetometer_y_data()
data_z = mag.get_magnetometer_z_data()

# get the health sensor
hlth = stn.health_sensor()
data_bat = hlth.get_battery_charge_remaining_data()
data_temp = hlth.get_internal_temp_c_data()
data_net = hlth.get_network_type_data()

# get the location sensor
loc = stn.location_sensor()
data_lat = loc.get_latitude_data()
data_lon = loc.get_longitude_data()
data_alt = loc.get_altitude_data()
```

Refer to these [tables](04a_sensor_units.md) for information on the possible channels for each sensor, as well as the
units for each channel.

If you encounter any issues while accessing a Sensor, refer to the page on
[Troubleshooting](troubleshooting.md#unexpected-return-values-from-functions)

You have finished the DataWindow examples.  Click here to view the [next steps](what_to_do_next.md).