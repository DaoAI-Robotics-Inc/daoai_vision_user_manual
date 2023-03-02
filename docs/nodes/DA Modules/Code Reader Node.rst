Code Reader Node 
==================

Overview
----------

Many industries label products using symbols from symbologies such as bar codes and QR codes. 
This is done for identification purposes during different stages of production and distribution. 

**Code Reader Node** is implemented to detect and decode codes in grayscale images.


The supported code types are:

.. list-table:: 
   
   *  - .. figure:: images/code_reader/codebar.png

           Codabar

      - .. figure:: images/code_reader/maxi.png

           2D Maxicode

      - .. figure:: images/code_reader/aztec.png

           2D Aztec

      - .. figure:: images/code_reader/upca.png

           UPC-A

      - .. figure:: images/code_reader/gs1_128.png

           GS1-128

   *  - .. figure:: images/code_reader/planet.png

           Planet

      - .. figure:: images/code_reader/upce.png

           UPC-E

      - .. figure:: images/code_reader/micropdf417.png

           2D MicroPDF417

      - .. figure:: images/code_reader/pdf417.png

           2D PDF417

      - .. figure:: images/code_reader/qr_code.png

           2D QR

   *  - .. figure:: images/code_reader/codes_2d_truncatedpdf417.png

           2D Truncated PDF417

      - .. figure:: images/code_reader/codes_1d_code128.png

           Code 128

      - .. figure:: images/code_reader/bc412.png

           BC412

      - .. figure:: images/code_reader/codes_2d_datamatrix.png

           2D Data Matrix

      - .. figure:: images/code_reader/codes_1d_ean13.png

           EAN 13

   *  - .. figure:: images/code_reader/codes_1d_ean14.png

           EAN 14

      - .. figure:: images/code_reader/codes_2d_microqrcode.png

           2D Micro QR

      - .. figure:: images/code_reader/codes_1d_posnet.png

           Postnet

      - .. figure:: images/code_reader/codes_1d_code39.png

           Code 39

      - .. figure:: images/code_reader/codes_1d_ean8.png

           EAN 8

   *  - .. figure:: images/code_reader/codes_1d_4_state.png

           4-state

      - .. figure:: images/code_reader/codes_1d_pharmacode.png

           Pharmacode

      - .. figure:: images/code_reader/codes_1d_industrial_25.png

           Industrial 2 of 5 (standard 2 of 5)

      - .. figure:: images/code_reader/codes_1d_rss.png

           GS1 Databar

      - .. figure:: images/code_reader/codes_1d_interleaved25.png

           Interleaved 2 of 5 (ITF-14)

   *  - .. figure:: images/code_reader/codes_1d_code93.png

           Code 93
      
      -

      -

      -

      -

Input and Output 
--------------------
	
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------------+
| Input                                  | Type                          | Description                                                                         |
+========================================+===============================+=====================================================================================+
| Image In                               | Image                         | A input grayscale image (can use Image Process node to convert images to grayscale) |
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------------+


+-------------------------+-------------------+------------------------------------------------------------------------+
| Output                  | Type              | Description                                                            |
+=========================+===================+========================================================================+
| numCodeRead             | Int               | The number of code found in the input image                            |
+-------------------------+-------------------+------------------------------------------------------------------------+
| decodedString           | Vec<String>       | The decoded String vector of the Codes found in the image              |
+-------------------------+-------------------+------------------------------------------------------------------------+

Node Settings 
----------------

   .. image:: images/code_reader/settings.png
      :scale: 100%
|

   * Num to Detect: 
      The number of codes to detect in the image. 
      Only 1D code types (excluding GS1 Databar, 4-state, Planet, and Postnet code types) and the 2D data Matrix code type support searching for multiple occurrences.

   * Code Type:
      Selet the Code Type to detect in the image from a dropdown list.

Advance Settings 
~~~~~~~~~~~~~~~~

   * foreground_color: 
      Sets the foreground color of the code. 

   * threshold_mode: 
      Sets the threshold mode used to internally binarize the source image.

   * threshold_value (Range: [0, 255]): 
      Sets the threshold value used to internally binarize the source image, depending on the specified threshold mode. Note that if THRESHOLD_MODE is set to ADAPTIVE, this control type is ignored

   * minimum_contrast (Range: [1, 255]): 
      Sets the minimum possible contrast between the foreground and background in the target image for 1D codes (excluding Planet and Postnet) when using the ADAPTIVE threshold mode. Increasing the minimum contrast will typically improve code detection, particularly in the presence of noise and non-uniform lighting.However, if the minimum contrast is higher than the contrast of a code, the code will not be read correctly.For 2D codes, the minimum contrast is determined automatically, so the adaptive threshold mode does not use the minimum_contrast setting.

   * speed: 
      Sets the search speed. The faster the search speed, the less robust the operation. For 1D code types, consider reducing the search speed when the pixel height of the bar code is small.For 2D code types, consider reducing the search speed when the cell size is small relative to the image size.

   * time_out: 
      Specifies the maximum decoding time for an detection, in msec. default is 2000.

   * error_correction (Range: [5, 95]): 
      Sets the type of error correction. This field will change base on different code type.
      Only 2D Aztec code type support percentage correction. 

   * check_quiet_zone: 
      Sets whether the presence of the quiet zone is necessary for a successful detection of this code type. 

   * string_format: 
      Sets the format of the output of the string.

   * search_angle_value (Range: [0, 360]): 
      Sets the nominal search angle. default is 0.

   * search_angle_step (Range: [0.1, 180.0]): 
      Sets the angle increment/decrement used when searching for a 1D code through an angular range.

   * search_angle_delta_neg: 
      Sets the negative angular range of the search.

   * search_angle_delta_pos: 
      Sets the positive angular range of the search.

Search Region
~~~~~~~~~~~~~~~~

   Can click "Define Search Region" to graphically define the region on the display window.
   
   * Top Left X:
      The top-left pixel's x value.

   * Top Left Y:
      The top-left pixel's Y value.

   * Size X:
      The width of the region starting from top-left x.

   * Size Y:
      The height of the region starting from top-left y.

Procedure to Use
------------------

1. First prepare the input grayscale image, can use image process node to convert the RGB image to grayscale using Colours/To Gray operation.

2. Right-click the node where you want to add the Code Reader node after, and insert Code Reader node. 

   .. image:: images/code_reader/step_2.png
      :scale: 80%
|

3. Link the input image to the output of your Image Process node.

   .. image:: images/code_reader/step_3.png
      :scale: 90%
|

4. Select the Code Type From the dropdown list. Will use 2D QR as an example.

   .. image:: images/code_reader/step_4.png
      :scale: 80%
|

5. Then you can run the node, and the node will detect for QR code in the input image.

   .. image:: images/code_reader/step_5.png
      :scale: 60%
|

6. You may optionally adjust the advanced settings or define a search region in the image.








