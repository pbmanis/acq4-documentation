.. _userTutorialsPatching:

Patching a Cell
===============

This tutorial describes a typical procedure for patching a neuron using the :ref:`Patch module<userModulesPatch>` and  :ref:`Data Manager module<userModulesDataManager>`.

1. Open the :ref:`Data Manager module<userModulesDataManager>` and create a new folder to hold the data for a single cell. The new folder should be highlighted in red to indicate that all modules will store data to that location. See the :ref:`userTutorialsDataOrganization` tutorial for more on this topic.
2. Open the :ref:`Patch module<userModulesPatch>` configured for the clamp channel you will be using.
1. Place electrode in the bath, click **Reset History** and **Bath**. 
2. Correct the pipette offset at the amplifier.
3. Begin sealing onto a cell. When the input resistance measurement exceeds 100 MΩ, click **Patch**.
4. Monitor the input resistance as it increases to > 1 GΩ. 
5. Adjust pipette compensation at the amplifier.
6. Rupture the cell membrane.
7. Press **Cell** and check for appropriate resting membrane potential, input resistance, and access resistance.
8. Press **Monitor** 

