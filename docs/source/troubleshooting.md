# Troubleshooting

Refer to this page for common fixes to problems using DataWindow.

## First Things First

* [Check if the redvox SDK is installed](getting_data.md#python-setup).

## Enable Error Reporting

* Enable the debug parameter in DataWindow to display any errors encountered while creating DataWindow.
```python
from redvox.common.data_window import DataWindow

my_event_name: str = "event_name"

datawindow = DataWindow(event_name=my_event_name,
                        # ...
                        debug=True)
```

* Use the `print_errors()` function of DataWindow to display any errors.
```python
from redvox.common.data_window import DataWindow

my_datawindow: DataWindow = DataWindow()

my_datawindow.print_errors()
```

## Check Your Code

* If you can't access the DataWindow class, include this line to import DataWindow into your project:
  `from redvox.common.data_window import DataWindow`

* If you can't access the DataWindowConfig class, include this line to import DataWindowConfig into your project:
  `from redvox.common.data_window import DataWindowConfig`

* Check the value of the `input_dir` parameter in the DataWindowConfig for any errors.

* Check that you are using the [appropriate value](00_create_data_window.md) for the `structured` parameter of DataWindowConfig.

* Check all the parameters of DataWindow and DataWindowConfig for any errors.

* Check the value of any station IDs when using them in DataWindow parameters or retrieving the data.  IDs may look 
  similar to each other.

* If the results are not what you expect, try adjusting the parameters of DataWindow.  
  Refer to [DataWindow with Parameters](00a_data_window_parameters.md#simplified-datawindow-with-parameters)
  for an example on how to set the most commonly used parameters.
  Timestamps are in [UTC](https://www.timeanddate.com/time/aboututc.html).  You may use the 
  [date time utilities](https://redvoxinc.github.io/redvox-sdk/api_docs/redvox/common/date_time_utils.html)
  provided in `redvox.common.date_time_utils` to convert UTC epoch times into datetimes.

## Unexpected Return Values from Functions

* Any function that returns a Station or Sensor could return None, as that Station or Sensor may not exist. 
  Update the parameters of the function or use a different function as needed.

* You may get a list of channel names when accessing data in a Sensor.  This means that the channel you are trying to 
  access in the Sensor does not exist.  Use one of the listed channel names.

* Timestamps are often adjusted from the raw data values due to differences in device clock timing.  You may access the
  raw data values using the `unaltered_data_timestamps()` function.  See example below:

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# get the first station
stn = dw.first_station()

# get from a specific sensor
audio = stn.audio_sensor()
audio_timestamps = audio.unaltered_data_timestamps()

# get from all sensors
sensors = stn.get_station_sensor_types()
for s in sensors:
    timestamps = stn.get_sensor_by_type(s).unaltered_data_timestamps()
```

## Check Your Data

* Check that the files within the input directory are in one of two formats 
  ([structured or unstructured](00_create_data_window.md)) described in the 
  [Creating a DataWindow](00_create_data_window.md) example.
  Use the appropriate value for the `structured` parameter of DataWindowConfig.

* When working with structured directories, ensure that all API 1000 (API M) files are in a directory called `api1000`
  and all API 900 files are in a directory called `api900`.  API 1000 files end in `.rdvxm` and API 900 files end in `.rdvxz`

* Check your files for non-typical extensions.  `.rdvxm` and `.rdxvz` are the two expected file extensions.
  If you have other file extensions, those files may not work with DataWindow.

## Loading Existing DataWindows

* If you are loading a DataWindow from an existing file, [make sure you use the correct function](00b_save_load_data_window.md#loading-a-pre-constructed-datawindow).

* If you are still unable to load the DataWindow, compare the DataWindow's sdk_version() with the version you
  have installed.

```python
import redvox
from redvox.common.data_window import DataWindow

dw = DataWindow.load("path/to/file.json")

print("Installed Version: ", redvox.version())

print("DataWindow Version: ", dw.sdk_version())
```

* If the DataWindow's version is not equal to the SDK's version, [re-create the DataWindow](00_create_data_window.md).

* If you downloaded a DataWindow file from [redvox.io](https://redvox.io), use the website to re-run the report if able.

## If All Else Fails

Contact the developers.