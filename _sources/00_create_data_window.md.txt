# Create a DataWindow

In this example we will demonstrate how to create a DataWindow using raw data files.

> **_Please note:_**
> 
> Raw data files are stored in one of two ways:
> * Structured: Files are organized by date and time as specified in the
    [API-M repo](https://github.com/RedVoxInc/redvox-api-1000/blob/master/docs/standards/filenames_and_directory_structures.md#standard-directory-structure).
> * Unstructured: All files exist at the same level in the directory.
> 
> Raw data files come in specially formatted files with one of the following extensions: `.rdvxz` or `.rdvxm`.

If you have downloaded a pre-constructed DataWindow, then please visit the 
[Load DataWindow](00b_save_load_data_window.md#loading-a-pre-constructed-datawindow) section.

## Loading Raw Data

> **_Please note:_** Creating a DataWindow will take longer to complete the more data being used to create it.  Please 
> have patience when reading large amounts of data.

This example shows how to load raw data files in a structured layout.

```python
from redvox.common.data_window import DataWindow, DataWindowConfig

# Input Directory
input_dir = "path/to/redvox/data"

# Configuration for DataWindow
dw_config = DataWindowConfig(input_dir=input_dir, structured_layout=True)

# Create the DataWindow
dw = DataWindow("my_dw", config=dw_config)
```

This example shows how to load raw data files in an unstructured layout.

```python
from redvox.common.data_window import DataWindow, DataWindowConfig

# Input Directory
input_dir = "path/to/redvox/data"

# Configuration for DataWindow
dw_config = DataWindowConfig(input_dir=input_dir, structured_layout=False)

# Create the DataWindow
dw = DataWindow("my_dw", config=dw_config)
```

You may want more control over which data is loaded into DataWindow.  Please view the 
[DataWindow Parameters](00a_data_window_parameters.md) example for more details.

Now that you have a DataWindow, we will demonstrate how to [access the metadata](01_data_window_metadata.md) in the 
next section.
