.. RedVox SDK Examples documentation master file, created by
   sphinx-quickstart on 2022 Jun 7.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Redvox SDK DataWindow Examples
================================

Welcome to Redvox SDK DataWindow Examples!

This is a space for examples and tutorials of DataWindow from the `RedVox SDK <https://github.com/RedVoxInc/redvox-python-sdk>`_.

DataWindow is a format-agnostic curator of raw data files that is designed to provide the most complete set of data it
can find to the user as efficiently as possible.  The process of creating a DataWindow involves many steps and validation
checks.  You may find details about the process in the
`DataWindow Documentation <https://github.com/RedVoxInc/redvox-python-sdk/tree/master/docs/python_sdk/data_window>`_.

Contents
----------

**Setup**

- :doc:`prereqs`
- :doc:`getting_data`

**DataWindow Basics**

- :doc:`what_is_data_window`
- :doc:`00_create_data_window`
- :doc:`01_data_window_metadata`
- :doc:`02_station`
- :doc:`03_station_data`
- :doc:`04_sensor_data`

**DataWindow Advanced**

- :doc:`00a_data_window_parameters`
- :doc:`00b_save_load_data_window`
- :doc:`03a_time_synchronization`
- :doc:`03b_event_data`
- :doc:`04a_sensor_units`
- :doc:`troubleshooting`

Basic definitions
------------------

The following terms are common terminology used throughout this documentation.

- **RedVox**: Not the NYC based rock band. RedVox refers to products developed by `RedVox, Inc. <http://nelha.hawaii.gov/our-clients/redvox/>`_.

- **redvox.io**: the RedVox webpage where RedVox reports are done. Visit `redvox.io <https://redvox.io/#/home>`_.

- **RedVox Report**: `redvox.io <https://redvox.io/#/home>`_ can perform the sensor analysis
  (plot audio waveforms, spectrograms, state of health data) for you and provide a summary - a report.

- **RedVox Infrasound Recorder**: A smartphone app that can record audio and other stimuli such as pressure.
  Visit `RedVox Sound <https://www.redvoxsound.com>`_ to learn more about the app.

- **RedVox Python SDK**: A Software Development Kit (SDK) developed to read, create, edit, and write RedVox files
  (files ending in `.rdvxz` for `RedVox API 900 <https://bitbucket.org/redvoxhi/redvox-protobuf-api/src/master/>`_
  files and `.rdvxm` for `RedVox API 1000 <https://github.com/RedVoxInc/redvox-api-1000>`_ files). Visit
  `GitHub RedVox Python SDK <https://github.com/RedVoxInc/redvox-python-sdk>`_ to learn more about the SDK.

- **Station**: a device used to record data, e.g., a smartphone recording infrasound waves using the
  `RedVox Infrasound Recorder <https://www.redvoxsound.com/>`_ app. Also a Python class designed in the RedVox Python SDK to
  store station and sensor data. Visit
  `Station Documentation <https://github.com/RedVoxInc/redvox-python-sdk/tree/master/docs/python_sdk/data_window/station>`_
  for more information on the Station Python class. A station has sensors (see below).

- **Sensor**: a device that responds to a physical stimulus, e.g., barometer, accelerometer. The units for each available sensor can
  be found in `RedVox SDK Sensor Documentation <https://github.com/RedVoxInc/redvox-python-sdk/tree/master/docs/python_sdk/data_window/station#sensor-data-access>`_.
  A station should always have audio sensor (and hence audio data).

- **Epoch** or **epoch time**: unix time (also referred to as the epoch time), the number of seconds since 1 January 1970.
  For example the epoch time for Thursday, July 1, 2021 at 9:00:00 am UTC would be 1625130000.

.. toctree::
   :maxdepth: 2
   :caption: Before Starting...
   :hidden:

   prereqs
   getting_data

.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: DataWindow Basics...

   what_is_data_window
   00_create_data_window
   01_data_window_metadata
   02_station
   03_station_data
   04_sensor_data

.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: DataWindow Advanced...

   00a_data_window_parameters
   00b_save_load_data_window
   03a_time_synchronization
   03b_event_data
   04a_sensor_units

.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: For more information:

   what_to_do_next
   troubleshooting
