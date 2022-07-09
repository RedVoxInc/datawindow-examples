# Time Synchronization

Time synchronization is the process of adjusting raw data timestamps to more accurately represent when the data was 
recorded.  This is due to inherent drift in the clocks of devices; that is, not all clocks update their time equally.

## Getting Time Synchronization Data

This example shows how to access time synchronization data from a Station.

```python
from redvox.common.station import Station

# Replace the following line with an appropriate method of loading station data
stn: Station

# get the time synchronization data
ts = stn.timesync_data()

# Print the time synchronization exchanges
print(ts.sync_exchanges())

# Print the best latency (for the SDK, it's the lowest)
print(ts.best_latency())

# Print all latencies
print(ts.latencies())

# Print the best offset (for the SDK, it's the offset paired with the lowest latency)
print(ts.best_offset())

# Print all offsets
print(ts.offsets())

# Print the mean latency of the data
print(ts.mean_latency())

# Print the mean offset of the data
print(ts.mean_offset())
```

## Keeping Accurate Time

According to the [NTP standard](https://www.ntp.org/), clocks have various degrees of accuracy based on the source of 
their time.  We assume an NTP clock with a low-numbered stratum is very close to the actual time, and will adjust 
timestamps using that as a reference.  To do this, we use a tri-message exchange to give us an idea of how much offset 
there is between a recording device's clock and an NTP server's clock.

## Tri-Message Exchange

A tri-message exchange consists of 3 exchanges sent in a series between a server and a device.  The first message 
comes from the server, and the device responds, followed by the server responding with one more message.  Whenever a 
message is sent or received, the computer sending or receiving the message adds a timestamp based on its clock to the 
exchange.  The end result is 2 sets; 3 timestamps from the server and 3 timestamps from the device.

## Calculating the Offset

We will label the server timestamps as A1, A2, and A3, in ascending order.  We will label the device timestamps as B1, 
B2, and B3, in ascending order.  Therefore, the timestamps are created in this order: A1, B1, B2, A2, A3, B3.  We can 
now estimate the difference in time, or offset, between the server and the device using these equations:

> Offset between server and device: (A1 - B1 + A2 - B2) / 2
> 
> Offset between device and server: (A3 - B3 + A2 - B2) / 2

We use the average of the two values to determine the offset during that specific tri-message exchange.

For a given DataWindow, we consider the offset that is paired with the lowest latency as the best representative offset 
of the DataWindow.

## Using the Offset to Update Timestamps

We update our raw data timestamps by adding the offset to each.  This allows us to account for offsets that are less 
than 0 (meaning the device time is ahead of the server's).

Return to the section on how to [access the data](03_station_data.md).
