How to deal with workspace upgrading
============

Workspace might have possibility of being corrupted. 
Especially when switching between versions, modified nodes would cause system crash and/or workspace corrupted. 
This could cause data lost and corruption. 

.. note:: 
    Vision Studio newer than 2.22.2.0-146 do **NOT** have this issue. If you are switching from older versions, please follow the article to avoid potential data lost and workspace corruption.

When you update your Vision Studio, there are 2 kinds of updates:

    #. Update to newer version of **Vision Studio**, this update requires uninstall old version to install new updates;
    #. Patches update, this update executes an **exe** file and does not require uninstall the old versions;

Upgrade Checklist
------------------

When you upgrade **Vision Studio**, you should follow the steps below to ensure the older version is deleted and does not influence the newer version stability. 
Use the exact same version of application that you help them upgrade to build a new workspace that has the same functionality and same robot communication protocol. 

    #. Restart PC
    #. Uninstall **Vision Studio** or **WeRobotics** (In older versions there might exist multiple application and need to uninstall all of them from control panel)
    #. Uninstall DaoAI Camera
    #. Make sure nothing is in previous installing folder
    #. Install newest WeRobotics application
    #. Install matching DaoAI Camera
    #. Check if .yml calibration files need to upgrade (Either edit yml file to match the current yml version or do calibration again using newest software)
    #. Open upgraded workspace
    #. Generate new .cfg camera setting file.
    #. Update Robot Communication if choose to use newer protocol

When you install the new update, there is a update document states what nodes have updated. 
When your old workspace has this node, you will need to delete this node then re-insert the node in order to prevent potential workspace corruption issue. 

For example, you are currently using 2.21.10 version **Vision Studio**, and you receive the update of version 2.22.2.0 which has updates in ``Gripper`` node. 

.. image:: Images/delete.png
    :align: center 

|

Then insert the new ``Gripper`` node into the flowchart to avoid potential corruption.

There is another way to possibly occur workspace corruption or system crashes: loading the old-version files(such as yml and cfg files). 
In version 2.21.4 **Vision Studio**, it has different parameters for yml file; if you are loading this yml file in newer version could cause serious issues. 

Therefore, make sure you read the update notes between versions or use the update-to-date files. 

Potential file types of causing this issue:

    #. **yml** file -> calibration file
    #. **cfg** file -> camera configuration file


