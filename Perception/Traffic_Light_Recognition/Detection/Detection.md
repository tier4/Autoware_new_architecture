Detection
=====
# Role

Detection module in Traffic Light Recognition finds traffic lights' region of interest(ROI) in the image. For example one image could contain many traffic signals at intersection. However, the number of traffic signals in which an autonomous vehicle is interested is limited. Map information is used for which part of an image needs to be paid attention to.

## Input

| Input       | Data Type
|-|-|
| Camera       | `sensor_msgs::Image`|
|Camera info | `sensor_msgs::CameraInfo`|
|Map | `autoware_lanelet2_msgs::MapBin`|
|TF | `tf2_msgs::TFMessage`|

## Output

| Output       | Data Type| Output Module |
|----|-|-|
|Cropped traffic light ROI information|`autoware_perception_msgs::TrafficLightRoiArray.msg`|Traffic LIght Recognition: Classification|

## Design
The Detection module is designed to modularize some patterns of detecting traffic lights' ROI.

![msg](/img/LightDetectionDesign.png)

This is our sample implementation for the Detection module.
![msg](/img/LightDetectionDesign2.png)

Our sample implementation has one advantage over only Map Based Detection method, which sometimes suffers from calibration error. In our approach, Map Based Detection passes rough ROIs to Fine Detection so that it would not care minor calibration error. Fine Detection refines the passed rough ROI to accurately cropped traffic signals' ROI.