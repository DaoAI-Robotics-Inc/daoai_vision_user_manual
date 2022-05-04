Procedure of Using Code Reader Node
=====================================

1. (If needed) convert input image from RGB to gray scale using image process node.
2. Link "Image In" field to the gray scale image. Run the node once. You will see the original image on the display.
3. Select the code type and number of occurrences to find. Optionally, define a search region on the image by clicking on "Define Search Region" button and draw a rectangle ROI on display.
4. Run the node again. Now you should see the found code region with the decoded string in the middle.
5. Optionally, adjust advanced parameters to get better result. See the definition of advanced parameters in overview page.
6. Use the decoded string to define further picking action. For example, run different flowchart branch based on the string from the code.