.. _userConfiguration:

Configuration
=============

Configuring ACQ4 involves editing '.cfg' files in the *config* directory. In these files, you may define:
    
* The devices in your system
* The list of loadable modules 
* Data storage locations
* Per-user configurations
    
When ACQ4 is started, it first checks to see whether a configuration file has been specified on the command line using the ``-b`` flag. Next, it searches through the following paths looking for a 'default.cfg' file:

* ACQ4_package_root/config/
* ACQ4_package_root/../config/
* /etc/acq4   (unless running on Windows)
* ACQ4_package_root/config/example/
* ACQ4_package_root/../config/example/

The last two paths in the list are possible locations of example configuration files included with ACQ4. The example configuration contains examples of every kind of device supported in ACQ4. Most of these entries are disabled in the configuration; the active devices can be run without any hardware to demonstrate the capabilities of ACQ4. 

The fastest way to get started with a fresh installation is to run ACQ4 (by running ``python -m acq4`` or ``acq4`` or by clicking a shortcut, depending on your method of installation). If ACQ4 is running from an example configuration, a message will be displayed giving the location of this configuration. Copy all files from this location into its parent 'config' directory, and begin editing (a source code editor is very helpful here).

.cfg File Syntax
----------------

It is important to first understand that a 'configuration' is a single document, but for organization this document is often split up across multiple .cfg files. At its most basic level, a configuration is a list of name:value pairs:
    
::
    
    storageDir: "/home/user/data"
    protocolDir: "config/protocols"
    
In the example above, the name "storageDir" is assigned the value "/home/user/data".
Values may also contain nested lists of name:value pairs:
    
::
    
    Camera:
        driver: 'PVCam'
        serial: 'PCICamera0'
        parentDevice: 'Microscope'
        exposeChannel:                  # Channel for recording expose signal
            device: 'DAQ'
            channel: '/Dev1/port0/line0'
            type: 'di'

In this example, we have Camera.driver = 'PVCam', Camera.serial = 'PCICamera0', Camera.exposeChannel.device = 'DAQ', and so on. This syntax allows the creation of arbitrarily complex hierarchies of configuration data. *Note that each nested level must have the same number of indentation spaces for each line*.

Since this configuration tree can become quite large and complex, it is often useful to break off the larger branches and move them to a file of their own:
    
::
    
    folderTypes: readConfigFile('folderTypes.cfg')
        
This example would read the entire contents of 'folderTypes.cfg' and insert that as the value for 'folderTypes'.

Further notes about this syntax:
    
    * You can use "double" or 'single' quotes, but not "both'
    * File or directory names should be quoted and use forward slashes (/) on Linux and OSX or double-back slashes (\\\\) on Windows (eg "/home/user/data" or "C:\\\\data\\\\user").
    * Some options will call for a list of values. This can be given just by separating the values with commas inline like ``value1, value2`` or with brackets like ``[value1, value2]``
    * Finally, you may add comments to .cfg if they are preceded with a hash (#) symbol
    
    

Configuration Structure
-----------------------

When ACQ4 first starts, it searches a few default locations for a file named 'default.cfg' (it is possible to override this with the ``-c`` flag). The structure of this file should look like:
    
::
    
    storageDir: "storage/dir" 
    modules:
        ...
    devices:
        ...
    folderTypes: 
        ...
    configurations:
        ...
        
In this format, the storageDir specifies the *default* location where data should be stored when no other location is specified. All other sections are discussed below:
    
.. _userConfigurationModules:

Modules Configuration
'''''''''''''''''''''

Loading a module requires knowing both the name of the module and specifying a specific set of configuration options for the module to use. For example, I have a patch clamp amplifier with two channels. When I load the *Patch* module, I need to specify whether it should use channel 1 or channel 2. To make this process easier for the end user, we define a list of pre-configured modules which the user may choose from. These names appear in the Manager module as the list of loadable modules.

The format for defining a pre-configured module is:
    
::
    
    UniqueName:
        module: "ModuleName"
        config:
            ...config options...
        shortcut: "shortcut key"

Here, *ModuleName* must refer to one of the modules defined in the directory **lib/modules**. The exact options specified under *config* will differ depending on the module being loaded. The *shortcut key* specifies a keyboard shortcut that can be used to raise the module's window (for example: 'F2', 'Ctrl+M', or 'Alt+Enter'). Taking this example, a very common module list might look like this:
    
::
    
    modules:
        Data Manager:
            module:  'DataManager'
            shortcut: 'F2'
        Task Runner:
            module: 'TaskRunner'
            shortcut: 'F6'
            config:
                ## Directory where Task Runner stores its saved tasks.
                taskDir: 'config/example/tasks'
        Camera:
            module:  'Camera'
            shortcut: 'F5'
        Patch Clamp 1:
            module: 'Patch'
            shortcut: 'F3'
            config:
                clampDev: 'Clamp1'
        Patch Clamp 2:
            module: 'Patch'
            shortcut: 'F4'
            config:
                clampDev: 'Clamp2'

Note in this example that the name 'Camera' is used 3 times to refer to 3 different things: 1) the name of the preconfigured module that will appear in the Manager user interface, 2) the name of the python module to load (ie, acq4.modules.Camera), and 3) the name of the camera device that should be used by this module when it is loaded.


.. _userConfigurationDevices:

Devices Configuration
'''''''''''''''''''''

The format for defining a device is:
    
::
    
    UniqueName:
        driver: "deviceType"
        ...
            
Here, *deviceType* refers to one of the device types defined in the directory **acq4/devices** (examples: NiDAQ, MultiClamp, Microscope). Any further options will depend on the device, and are described in the documentation for that device type (see :ref:`userDevices`). Refer to the example configuration in **acq4/config/example**.


.. _userConfigurationFolderTypes:

FolderTypes Configuration
'''''''''''''''''''''''''

ACQ4 gives the user full control over deciding how best to organize their raw data as it is being collected. For example, a typical user might create a folder for every day they run experiments, and a sub-folder for every cell they record from. Each folder can be annotated by the experimenter, and often we want these annotations to be consistent from day to day. To facilitate this, we can define a set of folder types with a specific list of the data that should be annotated for each type. These types appear in the Data Manager module when adding new folders, and the annotations are automatically displayed as a form to be filled out by the experimenter. 

The basic syntax for a folder type is:
    
::
    
    UniqueName:
        name: 'storageName'
        info:
            ...
            
Here, *UniqueName* is the name that will appear in the Data Manager module list of folder types. *storageName* specifies how each new folder will be named as it is created, including the possibility for date formatting ("%Y.%m.%d"). *info* is a list of name:value pairs that specify the set of meta-data fields to be included with each folder type. There are two types of input that can be specified: 
    
::
    
    fieldName1: 'text', number_of_lines
    fieldName2: 'list', ['option1', 'option2', 'option3']
    
For either field type, information will be stored as plain text. If the field type is *list*, then the user will see a drop-down menu of options to choose from (although it will still be possible to type in any arbitrary response). If the field type is *text*, then the user will simply see an empty text box to type in. 

The following is a complete example of a folder type used to contain all data collected for a single day. The metadata fields for this folder type represent aspects of the experiment that are expected to be constant for the entire day::

    Day:                    
        name: "%Y.%m.%d"  # folder will be named YYYY.MM.DD
        info:
            description: "text", 6          
            species: "list", ["C57 Mouse", "CBA Mouse", "Rat"]
            age: "string" 
            sex: "list", ['M', 'F']
            weight: "string"
            temperature: "list", ['34C', '25C', '37C']
            solution: "list", ["Standard ACSF", "Physiological ACSF"]

For further reference, see the file config/example/folderTypes.cfg in the ACQ4 distribution.


Configurations Configuration
''''''''''''''''''''''''''''

Commonly, acquisition systems will be accessed by mutiple users requiring different configuration settings. One way to achieve this is to create a completely different set of configuration files for each user and specify which to use when starting the program. A simpler way is to define just the *differences* between these configurations and select them after the program has been started. 

The *configurations* section allows us to define a set of named modifications to the default configuration. For example: all users on a system want to use the same device and module configuration, but define their own data storage directory:
    
::
    
    configurations:
        Jeffrey:
            storageDir: 'C:\\data\\jeffrey'
        Walter:
            storageDir: 'C:\\data\\walter'
        Maude:
            storageDir: 'C:\\data\\maude'
        
In the example above, the three names would appear in the Manager module as loadable configurations. This allows each user to quickly select their storage settings. The settings for each user can be anything that would appear at the top-level configuration. Thus, users can specify their own folder types, preconfigured modules, etc (however devices may not be defined here). 



