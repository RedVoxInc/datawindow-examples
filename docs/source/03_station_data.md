# Accessing Station Data

In this example we will access data stored by the Station.

## Time Synchronization Data

Time synchronization data is used by the Station to correct its timestamps.  Read more about this process 
[here](03a_time_synchronization.md).

## Getting Time Synchronization Data from Station

This example shows how to access the time synchronization data in the Station.

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# get the first station
stn = dw.first_station()

# get the time synchronization data
ts = stn.timesync_data()
```

If you want to learn more about what you can do with the time synchronization data, visit [this page](03a_time_synchronization.md).

## Event Data

Events are signals of interest as determined by some algorithm or process.  They occur during operation of the Station 
and are identified on the device or via later analysis of the data.

## Getting Event Data from Station

This example shows how to access the Event data in the Station.

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# get the first station
stn = dw.first_station()

# get the events
events = stn.event_data()
```

If you want to learn more about what you can do with the Event data, visit [this page](03b_event_data.md).

We will demonstrate how to [access the sensor data](04_sensor_data.md) in the next section.