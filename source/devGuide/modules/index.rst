Modules
=======

Contents:

.. toctree::
    :maxdepth: 2
    
    Manager
    DataManager
    Camera
    Patch
    TaskRunner
    Imager
    Console

What is a Module?
-----------------

In short, a module is an almost-totally independent program which is launched by ACQ4 and has access to any of the services offered by ACQ4. Modules are free to do virtually anything they like--there are very few constraints on their code structure, behavior, appearance, etc. If the task you are trying to accomplish does not fit nicely into the existing modules, then it may be time to write a new one. 

How to Build a New Module
-------------------------

#. Create a new python module or package under acq4/modules. This can be a single file or a directory of files; it doesn't matter (but either way it must be *importable*). 
#. Create a subclass of acq4.modules.Module.Module. This should look something like::
    
    from lib.modules.Module import Module
    
    class NewModuleClass(Module):
        ...
        
#. Make your subclass importable as lib.modules.NewModuleClass.NewModuleClass. When loading your module, ACQ4 will issue the following statements to import your code and instantiate a new module::
    
    from lib.modules.NewModuleClass import NewModuleClass
    newMod = NewModuleClass(manager, name, config)

   When ACQ4 instantiates your module, it will pass in three arguments:
   
   * manager - a reference to the Manager that created the module. This object provides lots of useful services like getDevice(), getModule(), getCurrentDir(), and createTask().
   * name - the name assigned to this module. This helps to differentiate multiple instances of the same module class.
   * config - an arbitrary and optional configuration structure (usually a dict) which provides the module any other instantiation data it needs.


#. Define your class's __init__ function::
    
    class NewModuleClass(Module):
        def __init__(self, manager, name, config):
            Module.__init__(self, manager, name, config)  ## call superclass __init__
            ...

#. If your module creates a Qt window, give the module a window() method which returns a reference to the window. This allows ACQ4 to assign window keyboard shortcuts.

#. Optional: create a quit() method. This will be called when ACQ4 is quitting, allowing the module to clean up if needed.

#. Create a default configuration (or many) for loading your module. In the 'modules' section of your configuration files, add a new section that looks like::
    
    ModuleName:
        module: 'NewModuleClass'
        config:
            ...  (data here will be passed to the config 
            ...  argument when instantiating the class)
            
   Each section like this that you create adds a new entry to the main Manager window, allowing users to easily access the module.
   By changing the contents of the 'config' section, it is possible to allow multiple instances of the module to be loaded with different settings.


    
