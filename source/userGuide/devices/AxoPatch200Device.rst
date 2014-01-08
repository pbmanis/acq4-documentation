.. _userDevicesAxoPatch:
    
AxoPatch Devices
================

This device supports the use of the Axo Patch 200 amplifier. It requires a :ref:`DAQ device` to record from and output to each of the channels on the device. The following features are supported for the Axo Patch 200:
    
* Support for use with Patch module and Task Runner module.
* Assisted switching between recording modes. The Axo Patch 200 uses a manual switch to select between current- and voltage-clamp recording modes. When a module requires access to a specific recording mode, a dialog window pops up instructing the experimenter to set the clamp mode accordingly.
* Manages separate holding levels for current- and voltage-clamp modes; automatically selects correct holding value when switching between modes.
* Records from the **gain** channel on the amplifier and automatically scales electrode data accordingly. 
* Records LFP channel output as meta-data of electrode recordings.

Configuration Options
---------------------

::

    AxoPatch200:
        driver: 'AxoPatch200'
        config:
            ModeChannel: 
                device: 'DAQ' 
                channel: '/Dev1/ai13'
                type: 'ai'
            GainChannel: 
                device: 'DAQ' 
                channel: '/Dev1/ai14'
                type: 'ai'
            LPFChannel: 
                device: 'DAQ' 
                channel: '/Dev1/ai15'
                type: 'ai'
            Command: 
                device: 'DAQ' 
                channel: '/Dev1/ao0'
                type: 'ao'
            ScaledSignal: 
                device: 'DAQ' 
                channel: '/Dev1/ai5'
                type: 'ai'
            icHolding: 0.0
            vcHolding: -50e-3

The supported configuration parameters are:
    
* **driver** must be 'AxoPatch200'
* **config** contains required device-specific configuration options:
    * **ModeChannel**: :ref:`DAQ channel <userDevicesDAQGenericChannelSpecification>` connected to the Mode output.
    * **GainChannel**: :ref:`DAQ channel <userDevicesDAQGenericChannelSpecification>` connected to the Gain output.
    * **LFPChannel**: :ref:`DAQ channel <userDevicesDAQGenericChannelSpecification>` connected to the LFP output.
    * **Command**: :ref:`DAQ channel <userDevicesDAQGenericChannelSpecification>` connected to the Command input.
    * **ScaledSignal**: :ref:`DAQ channel <userDevicesDAQGenericChannelSpecification>` connected to the Scaled Signal output.

Manager Interface
-----------------


Task Runner Interface
---------------------
