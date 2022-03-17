
Overview
=========================

Input
-------------

* Cloud Ptr: point cloud used for classification
* Image Input: RGB image used for classification

Output
---------------

* classLabel: label of the object, an int defined by the deep learning model
* confidence: confidence of the classification

Classfication Setting
---------------------

* Model Mode: use only RGB for classification; use only depth(from point cloud) for classification; or use both.
* Model File Path: path to deep learning model
* Config File Path: path to deep learning config file