File Reading Crash
===============

By the time of this article publish, issue of reading null/broken file would cause system crash. There are some possibilities of corrupted files being loaded. 
And **Vision** does not have the capability to judge if the files are corrupted. Hence if **Vision** is trying to extract data from them, would have caused null pointer issue. 
We are working on this feature which **Vision** is able to detect if he file is corrupted and prevent system failure for better user experience. 

These are the list of files would be loaded by **Vision**, if the file type is fixed(**Vision** able to judge the data Validity) it would be put in ``red``.

Here is the list:
    * cfg => camera configuration setting file
    * ``daf => Digital Anchor File``
    * dcf => Multimedia File with Digit Right Management
    * stl => 3D printing and computer-aided design file(CAD)
    * obj => OBJFile
    * ``ply => Polygon File Format``
    * ``yml => Calibration File``
    * pt => Deep Learning Model File
    * txt => Text File
    * pcd => Point Cloud Model

If any hotfixes and patches in the future fixed any of the files with this crash issue, they woulde be mentioned in the patch notes as well as this article. 