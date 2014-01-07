.. _userDevicesCamera:
    
Camera Devices
==============

Support for scientific cameras currently includes all devices which use either PVCam (Photometrics) or QCam (Q-Imaging) drivers. Cameras support live-imaging modes as well as controlled data acquisition modes that specify the timing and behavior of the device. In live-imaging mode, the camera collects frames freely and sends them to a user-interface module for display. This mode is generally used for visualizing the preparation throughout the experiment including while navigating and during placement of electrodes for stimulating or patching. Cameras may also make use of connections to data acquisition channels. During task execution, the camera may be triggered by the data acquisition board or serve as the starting trigger for another device. 

In addition, many cameras export a TTL signal that indicates the timing of frame exposures. When it is recorded, this signal is analyzed to determine starting exposure time of each camera frame, allowing the precise synchronization of imaging and electrophysiology or other signals. Image data is stored to disk alongside the raw exposure and trigger signals, and the time values of each frame are stored as meta-data. The result is that physiological recordings made synchronously with imaging can be automatically registered temporally during analysis.

Cameras are treated by ACQ4 as optomechanical devices, and thus may be calibrated such that their size, position, and orientation have a fixed spatial relationship to any other optomechanical devices. This is most commonly used with both a motorized stage for position feedback and a microscope device which defines per-objective scaling and offset. With a properly configured system, image mosaics can be collected and automatically reconstructed.

Cameras support the following features:

* May be triggered by an arbitrary waveform generated on a DAQ digital output
* May be used to trigger the start of a DAQ acquisition
* Precisely timed frame acquisition by recording TTL exposure signal on a DAQ digital input
* Graphical interface for control via the Camera module
* Graphical interface for configuration via the Manager module
* Graphical interface for control via the Task Runner module

Note that the exact features available may differ depending on the capabilities of the camera hardware.


Camera device subclasses:
    
.. toctree::
    :maxdepth: 1
    
    QCamDevice
    PVCamDevice
    MockCameraDevice


Hardware Configuration
----------------------

Physical layout, triggering, exposure signals...

Note: If the exposure signal from the camera is connected to both DI and PFI ports, the DI recording may fail if the PFI is not being used.
This is because the PFI ports have very low impedance when unused.


Configuration Options
---------------------

The following is an example camera configuration:

::
    
    Camera:
        driver: '<driver name>'
        config:
            parentDevice: 'Microscope'
            transform:                          ## transform defines the relationship between the camera's
                                                ## sensor coordinate system (top-left is usually 0,0 and
                                                ## pixels are 1 unit wide) and the coordinate system of its
                                                ## scopeDevice
                position: (0, 0)
                scale: (1, 1)
                angle: 0

            exposeChannel:                                 ## Channel for recording expose signal
                device: 'DAQ'
                channel: '/Dev1/port0/line0'
                type: 'di'
            #triggerOutChannel: 'DAQ', '/Dev1/PFI5'        ## Channel the DAQ should trigger off of to sync with camera
            triggerInChannel:                              ## Channel the DAQ should raise to trigger the camera
                device: 'DAQ'
                channel: '/Dev1/port0/line1'
                type: 'do'
    


Manager Interface
-----------------

The :ref:`Manager user interface <userModulesManagerDevices>` for cameras typically consists of a simple list of parameters which define the current state of the camera. A standard set of parameters are available for all types of camera, including:
    
* **triggerMode** determines how the camera will decide when to begin frame exposures. Values are:
    
    * **Normal** a software signal begins frame acquisition, and the camera automatically determines when each frame exposure occurs.
    * **TriggerStart** a hardware trigger initiates frame exposure, and the camera automatically determines when each subsequent frame exposure occurs.
    * **Strobe** a hardware trigger initiates each frame exposure. The length of exposures is set by the **exposure** parameter.
    * **Bulb** A hardware trigger initiates each frame exposure, and the length of the TTL pulse determines the exposure time for each frame.
    
* **exposure** the current per-frame exposure time
* **binning** the number of sensor pixels that should be binned together to produce one output pixel. 
* **region** sets the region of interest on the sensor. Using a smaller region can result in faster frame transfer from the camera.

    .. figure:: images/Camera_ManagerInterface.png
    
Each camera driver implements extra parameters depending on the features available on the camera.

.. _userDevicesCameraTaskInterface:

Task Runner Interface
---------------------

    .. figure:: images/Camera_TaskInterface.png