# Event Data

Event data is all the sounds detected within the duration window.  A machine learning model is the source of the data.
The exact methods of detecting sounds are specific to each model, so the SDK uses a few tricks to store the data in a 
flexible way.

## Getting Event Data

Event data is accessed via the Station object.

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

Event data is organized into streams, with each stream identified by a unique name; usually a descriptor of the machine 
learning model that classified the events.  Streams also store metadata shared by all the events within the stream.

This example shows how to use the unique name to access the data of the stream.

```python
from redvox.common.event_stream import EventStreams

# Replace the following line with an appropriate method of loading event data from a Station
events: EventStreams

# Print the names of the streams
print(events.get_stream_names())

# Get a stream with a specific name
stream = events.get_stream("stream_name")
```

This example shows various functions you can use to access information about a stream.

```python
from redvox.common.event_stream import EventStream

# Replace the following line with an appropriate method of loading a stream
stream: EventStream

# Print the name of the stream
print(stream.name)

# Print the number of events in the stream
print(stream.num_events())

# Print the audio input sample rate
print(stream.input_sample_rate)

# Print the number of samples per window (the number of points the model needs to make a decision)
print(stream.samples_per_window)

# Print the number of samples per hop (how often the model starts a new window for detection)
print(stream.samples_per_hop)

# Print the version of the model used to detect the sounds
print(stream.model_version)

# Change the value below to the desired index
event_index = 0
# Print the event at a specific index
print(stream.get_event(event_index))

# Iterate over all events
for ev in stream.events:
    # Do something for each event
    print(ev)
```

This example shows various functions you can use to access Event information.

```python
from redvox.common.event_stream import Event

# Replace the following line with an appropriate method of loading a single Event
event: Event

# Print the name of the event
print(event.name)

# Print the timestamp of the event
print(event.get_timestamp())

# Print the data types and keys
print(event.get_schema())

# Print the data keys
print(event.get_data_keys())

# Print the data keys of string data
print(event.get_string_schema())

# Print the string data as a dictionary
print(event.get_string_values())

# Print the string data for a specific key
print(event.get_string_item("data_key"))

# Print the data keys of numeric data
print(event.get_numeric_schema())

# Print the numeric data as a dictionary
print(event.get_numeric_values())

# Print the numeric data for a specific key
print(event.get_numeric_item("data_key"))

# Print the data keys of boolean data
print(event.get_boolean_schema())

# Print the boolean data as a dictionary
print(event.get_boolean_values())

# Print the boolean data for a specific key
print(event.get_boolean_item("data_key"))

# Print the data keys of byte data
print(event.get_byte_schema())

# Print the byte data as a dictionary
print(event.get_byte_values())

# Print the byte data for a specific key
print(event.get_byte_item("data_key"))
```

## Event Structure

The Event class in the SDK is designed to be adaptable and prescient to future models.  The data for an event is split 
via the type of the data.  The data values are assigned keys based on the models' naming scheme and the ranking of the 
classifications.  We support multiple classifications for a single event, as the models' predictions aren't always 100% 
confident.  As the model's confidence in the classification is above a certain threshold (which can be adjusted in the 
app), we will store the information in the Event class.

As an example, a YAMNet model may be most confident that a certain sound is from an engine, but may also be fairly 
confident the sound is a vehicle, or even an animal roaring.  The data would look something like this:

```
{
 timestamp: 123456,
 data:
    {STRING: {class_0: engine, class_1: vehicle, class_2: animal_roar}
     NUMERIC: {duration: 975000.0, score_0: 0.9, score_1: 0.5, score_2: 0.2}
    }
}
```

In the above example, the score_X values correspond to the class_X values.  The higher the score, the more confident the 
model is about the sound being in the class.  This example shows how you would access the data:

```python
from redvox.common.event_stream import Event

# Replace the following line with an appropriate method of loading a single Event
event: Event

# Get the columns that start with "class"; i.e. "class_0", "class_1", "class_2"
classes = event.get_string_column("class")

# Get the columns that end with "0"; i.e. "class_0" and "score_0"
best_guess = event.get_classification(0)
```

Note how the classes were retrieved using the `get_string_column()` function.  We would not get any results if we had 
used a function that didn't retrieve string-typed data.  Take caution when retrieving Event data, as the type of the 
data you are retrieving matters greatly.  If you are stuck, use the `get_schema()` function or invoke each of the 
`get_X_schema()` functions, where X is one of string, numeric, boolean, or byte.

Return to the section on how to [access the data](03_station_data.md).
