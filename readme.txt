#image_proc_tegra

A ROS nodelet for image rectification using OpenCV's gpu functions. This nodelet is useful to reduce CPU usage in rectifying large video streams.
The OpenCV install linked by ROS must have the gpu apis (ie. compiled with gpu support or using OpenCV4Tegra)

same topics as image_proc:

```
Subscribed topics:
  ~camera_info
  ~image_raw

Published topics:
  ~image_rect
```


example launch file:

```
  <!-- nodelet manager from image stream -->
  <node pkg="nodelet" type="nodelet" name="nodelet_manager"  args="manager" />
  
  <node pkg="nodelet" type="nodelet" name="image_proc_test" args="load image_proc_tegra/RectifyNodelet camera_nodelet_manager" output="screen">
    <remap from="camera_info" to="/camera/color/camera_info" />
    <remap from="image_raw" to="/camera/color/image_raw" />
    <remap from="image_rect" to="/camera/color/image_rect" />
  </node>
```


Performance:

On a jetson TK1 this nodelet reduces CPU usage by about 0.75 compared to image_proc. It rectifies 1080p images at about 11fps.

License:

BSD