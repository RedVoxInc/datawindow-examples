# Save and Load DataWindow

![](../img/dw_fc_dw.png)

This example shows how to save a DataWindow to disk and load it from disk.

## Saving a DataWindow

DataWindow stores information about how and where to save itself to disk as metadata.  It uses this metadata when 
you invoke the save function.

This example shows how to view the metadata related to saving DataWindow.

```python
from redvox.common.data_window import DataWindow

# We assume you have already have a DataWindow.
# This line is a placeholder for whatever method you prefer to get the DataWindow you want to save.
dw: DataWindow

# Print the save format.  NONE means no saving.
print(dw.out_type())

# Print the save directory.
print(dw.save_dir())
```

This example shows how to change the metadata related to saving DataWindow.

```python
from redvox.common.data_window import DataWindow

# We assume you have already have a DataWindow.
# This line is a placeholder for whatever method you prefer to get the DataWindow you want to save.
dw: DataWindow

# possible options: 
# "NONE" means no saving
# "LZ4" is a compressed file
# "PARQUET" is a set of directories
# if you don't use one of the above 3, it defaults to "NONE"
new_out_type = "ONE_OF_THE_OPTIONS"
# Set the save format.
dw.set_out_type(new_out_type)

# Set the save directory.
dw.set_save_dir("new/save/dir")
```

This example shows how to save a DataWindow to disk.

```python
from redvox.common.data_window import DataWindow

# We assume you have already have a DataWindow.
# This line is a placeholder for whatever method you prefer to get the DataWindow you want to save.
dw: DataWindow

# Save the DataWindow
dw.save()
```

## Loading a Pre-Constructed DataWindow

Existing DataWindows can be loaded directly, which skips a lot of background work done when reading raw data files.
There are two methods used to load pre-constructed DataWindows.

This example shows how to load a pre-constructed DataWindow from a compressed file.

> **_Please note:_** compressed pre-constructed DataWindow files have the extension .pkl.lz4

```python
from redvox.common.data_window import DataWindow

# Input Path
input_path = "path/to/data_window.pkl.lz4"

# Load the DataWindow
dw = DataWindow.deserialize(input_path)
```

This example shows how to load a pre-constructed DataWindow from a directory with a .json metadata file.

> **_Please note:_** a pre-constructed DataWindow directory contains a file with extension .json and one of the 
> following: 
> * a .pkl.lz4 file
> * one or more directories

```python
from redvox.common.data_window import DataWindow

# Input Path
input_path = "path/to/data_window.json"

# Load the DataWindow
dw = DataWindow.load(input_path)
```

Now that you have a DataWindow, we will demonstrate how to [access the metadata](01_data_window_metadata.md) in the
next section.
