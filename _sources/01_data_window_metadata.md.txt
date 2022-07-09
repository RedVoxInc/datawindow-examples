# Viewing Data Window Metadata

In this example we will use the SDK to view basic information in a DataWindow.

If you have not created a DataWindow, visit the [creating a DataWindow](00_create_data_window.md) page.
If you have an existing DataWindow, visit the 
[saving and loading a DataWindow](00b_save_load_data_window.md#loading-a-pre-constructed-datawindow) page.
You must have performed this step before working with the examples on this page.

## Accessing DataWindow Metadata

Metadata provides a high-level description of DataWindow.  It is independent of the data recorded by sensors.

This example shows which functions are used to view the metadata of a DataWindow.

```python
from redvox.common.data_window import DataWindow

# Replace the following line with an appropriate method of loading data
dw = DataWindow()

# Print the name of the DataWindow
print(dw.event_name)

# Print the origin of the DataWindow's event of interest
print(dw.event_origin)

# Print the SDK version used to create the DataWindow
print(dw.sdk_version())

# Print the configuration parameters of the DataWindow
print(dw.config())

# Print the directory where the DataWindow will be saved to
print(dw.save_dir())

# Print the type of file the DataWindow will be saved as
print(dw.out_type())

# Print the Station ids in the DataWindow
print(dw.station_ids())

# Print the entire DataWindow metadata without station ids
print(dw)

# Print the entire DataWindow metadata in a neatly formatted fashion
print(dw.pretty())

# Print the entire DataWindow metadata as a Python dictionary
print(dw.as_dict())
```

Now that you have accessed the DataWindow metadata, we will demonstrate how to [access Stations](02_station.md) 
in the next section.
