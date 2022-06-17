# Accessing Stations in a DataWindow

In this example we will access the Stations in a DataWindow.

## What is Station

DataWindow separates its data by several layers, the first being Station.  Stations are groupings of sensors.

## Getting Stations from DataWindow

This example shows how to access the first Station in a DataWindow.

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# get the first station
stn = dw.first_station()
```

You can also iterate over each of the Stations in a DataWindow:

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# do something for each station
for stn in dw.stations():
    print(stn.id())
```

If you know the Station's ID, you can access it directly using:

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# Replace the string value with the id you're looking for
station_id = "id_number"

# get the station that matches the id
stn = dw.get_station(station_id)
```

If you get a `None` value from the previous example, the ID you're looking for does not exist in the DataWindow.  Try 
another ID or other DataWindow.

## Station Metadata

Every Station also has metadata that provides a high-level description of it.  Three metadata values are required for 
a Station to exist; `id`, `uuid`, and `start_date`.  The combination of these three values define a unique Station.

This example shows which functions are used to view the metadata of a Station.

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# get the first station
stn = dw.first_station()

# Print the station's id
print(stn.id())

# Print the station's uuid
print(stn.uuid())

# Print the station's start date
print(stn.start_date())

# Print the station's nominal audio sample rate in hz
print(stn.audio_sample_rate_nominal_hz())

# Print the names of the Station's sensors
print(stn.get_sensors())

# Print the types of sensors on the Station
print(stn.get_station_sensor_types())

# Print other metadata of the Station
print(stn.metadata())

# Print the metadata of the individual files used to create the Station
print(stn.packet_metadata())

# Print whether the Station's timestamps are updated from the raw data
print(stn.is_timestamps_updated())
```

Now that you have looked at Station metadata, we will demonstrate how to [access the data](00_station_data.md) in the
next section.