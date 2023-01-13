Disassemble Pose Node
=========================


Overview
-----------

The Disassemble Pose node outputs 3 translation numbers and 3-4 rotation numbers (in degrees) from a 4x4 homogeneous transformation matrix.

Three main conventions are available for the rotation numbers:

**Euler Angles**: 3-number representation in the orders: XYZ, XZY, YXZ, YZX, ZXY, ZYX, and ZYZ.

**Axis Angle**: 3-number representation of axis with angle magnitude.

**Quaternion**: 4-number representation of a quaternion rotation.

Input and Output
-------------------

+----------------------------------------+-------------------------------+--------------------------------------------------------------------------+
| Input                                  | Type                          | Description                                                              |
+========================================+===============================+==========================================================================+
| Pose (Robot Read)                      | Pose                          | The Pose object to be disassembled                                       |
+----------------------------------------+-------------------------------+--------------------------------------------------------------------------+

+----------------------------------------+-------------------+-------------------------------------------------------------------------------+
| Output                                 | Type              | Description                                                                   |
+========================================+===================+===============================================================================+
| posX                                   | Double            | Disassembled pose's translation on X-axis.                                    |
+----------------------------------------+-------------------+-------------------------------------------------------------------------------+
| posY                                   | Double            | Disassembled pose's translation on Y-axis.                                    |
+----------------------------------------+-------------------+-------------------------------------------------------------------------------+
| posZ                                   | Double            | Disassembled pose's translation on Z-axis.                                    |
+----------------------------------------+-------------------+-------------------------------------------------------------------------------+
| rotA                                   | Double            | Disassembled pose's rotation on X-axis.                                       |
+----------------------------------------+-------------------+-------------------------------------------------------------------------------+
| rotB                                   | Double            | Disassembled pose's rotation on Y-axis.                                       |
+----------------------------------------+-------------------+-------------------------------------------------------------------------------+
| rotC                                   | Double            | Disassembled pose's rotation on Z-axis.                                       |
+----------------------------------------+-------------------+-------------------------------------------------------------------------------+
| rotQ                                   | Double            | the rotation around the vector (only used for quaternion rotation).           |
+----------------------------------------+-------------------+-------------------------------------------------------------------------------+

Settings
-----------

- **Order** :
     Select from a dropdown list to choose the order of the generated pose. Orders are: XYZ, XZY, YXZ, YZX, ZXY, ZYX, ZYZ, Axis Angle and Quaternion. 

Procedure to Use
------------------

1. Right click the node where you want to insert and insert an Disassemble Pose node.
    .. image:: Images/disassemble_pose/step_1.png
|

2. Link the Input Pose (used Assemble pose node as an example) and select an Order.

3. Run the node an you will see the values printed on the console, you can also access them through outputs.
    .. image:: Images/disassemble_pose/step_3.png
|

    .. image:: Images/disassemble_pose/step_3_1.png
|


