# Silhouette Segmentation Approaches

More up to date and better organized information available on [our notion page](https://www.notion.so/Silhouette-Segmentation-Research-9bef2c8c302248c199b0fea73c872d3c).

The following is a practical comparison of various techniques of segmenting silhouettes/the general foreground from the background. It is intended as cursory research to inform which approach we use for extracting silhouettes for future installations. We will both compare based off specs/ collected data and share sample footage under various conditions. Important factors include: 

- Cost 
- Silhouette quality 
- multiple device support
- Ability to operate robustly under changing lighting conditions
- Range and FOV 
- Ease of development and Installation 
- Ability to deal with a variety lighting conditions

In general we explored two approaches: 

- Depth Camera: Using a depth camera then setting a 3D region of interest to extract the foreground. 
- Camera + Segmentation: Using a camera, depth or other wise, and then applying ML based segmentation to extract the silhouettes/foreground. 

## Depth Cameras

![all cameras](Assets/allCams.JPG "all cameras")

### Data

| Depth Camera          | Price USD | reported Range (M)  | FOV  (H x V) | Low light performance (1-5) | Outdoor performance (1-5) | Outdoor sillhoutte range Meters (good quality - edge) | Multi Camera | Mac | Win | linux | openFrameworks | touchDesigner | Unity  |
|-----------------------|-----------|---------------------|--------------|-----------------------------|---------------------------|-------------------------------------------------------|--------------|-----|-----|-------|----------------|---------------|--------|
| ZED                   | 450       | 0.5 - 20            | 90 x 60      | 1                           | 5                         | 3.3 - 5                                               | Yes          | N   | Y   | Y     | Needs Update   | Y             | Y      |
| Intel RealSense D435i | 199       | 10                  | 87 x 58      | 4                           | 5                         | 4.5 - 8.3                                             | Yes          | Y   | Y   | Y     | Y              | Y             | Y      |
| Azure Kinect DK NFOV  | 400       | 0.5 - 5.46          | 75 x 65      | 5                           | 3                         | 2.7 - 4.1                                             | Supported    | N   | Y   | Y     | NA             | NA            | NA     |
| Azure Kinect DK WFOV  |           | 0.25 - 2.88         | 120 x120     | 5                           | 2                         | 1.5 - 2.1                                             |              |     |     |       |                |               |        |
| Kinect v2             | 280       | 0.7–6               | 70.6 x 60      | 5                           | 1                         | 1.4 - 2.4                                             | Not Easily   | N   | Y   | N     | Y              | Y             | Y      |

### Comparison

Our subjective ranking

| Cost                  | Form Factor           | Low Light             | Indoor Performance    | Outdoor Performance   | Range                 | FOV                   | Ease of Development   |
|-----------------------|-----------------------|-----------------------|-----------------------|-----------------------|-----------------------|-----------------------|-----------------------|
| Intel RealSense D435i | Intel RealSense D435i | Azure Kinect DK       | Azure Kinect DK       | Intel RealSense D435i | Intel RealSense D435i | Azure Kinect DK       | Intel RealSense D435i |
| Kinect v2             | ZED                   | Kinect v2             | Kinect v2             | ZED                   | ZED                   | ZED                   | Kinect v2             |
| Azure Kinect DK       | Kinect v2             | Intel RealSense D435i | ZED                   | Azure Kinect DK       | Azure Kinect DK       | Intel RealSense D435i | ZED                   |
| ZED                   | Azure Kinect DK       | ZED                   | Intel RealSense D435i | Kinect v2             | Kinect v2             | Kinect v2             | Azure Kinect DK       |

### Footage + Notes

Note that you can find more sample footage for each approach in the assets folder.

##### Stereo Zed

![Zed](Assets/stereoZed/zed_form.JPG )

Indoor Conditions

![Indoor Conditions Stereo Zed](Assets/stereoZed/gifs/ZED_Indoor.gif "Indoor Conditions Stereo Zed")

Indoor Low Light

![Indoor Low Light Stereo Zed](Assets/stereoZed/gifs/ZED_Indoor_lowLight.gif "Indoor Low Light Stereo Zed")

Outdoor Close 3.3M

![Outdoor Close Stereo Zed](Assets/stereoZed/gifs/ZED_outdoor_close.gif "Outdoor Close Stereo Zed")

Outdoor Far 5M

![Outdoor Far Stereo Zed](Assets/stereoZed/gifs/ZED_outdoor_far.gif "Outdoor Far Stereo Zed")


**Notes**

- IR cut filter on sensor, if it was possible to remove it would open up more installation possibilities.
- When testing range outside it only extended 10M not the full 20. 
- Has a 3D scanning application in its SDK.
- Tends to merge the background with foreground, Example: if someone is walking close to a surface the surface distorts around the person. 


#### Intel RealSense

![Zed](Assets/IntelRealSense/intel_form.JPG )

Indoor Lights On

![Indoor Lights On Intel RealSense](Assets/IntelRealSense/gifs/realSense_Indoor.gif "Indoor Lights On Intel RealSense")

Indoor Lights Off

![Indoor Lights Off Conditions Intel RealSense](Assets/IntelRealSense/gifs/realSense_dark.gif "Indoor Lights Off Intel RealSense")

Indoor lowlight

![Indoor Lights Off Conditions Intel RealSense](Assets/IntelRealSense/gifs/realSense_lowLight.gif "Indoor Lights Off Intel RealSense")


Outdoor Close 4.5 M

![Outdoor CloseIntel RealSense](Assets/IntelRealSense/gifs/realSense_outdoor_close.gif "Outdoor Close Intel RealSense")

Outdoor Far 8.3 M

![Outdoor Far Intel RealSense](Assets/IntelRealSense/gifs/realSense_outdoor_far.gif "Outdoor Far Intel RealSense")

Sillhouttes extracted with depth Thresholding 

![Sillhouttes extracted](Assets/IntelRealSense/gifs/realSenseSillhouttesUnprocessed.gif "Sillhouttes extracted with depth Thresholding ")

![Sillhouttes Extracted and Vectorized](Assets/IntelRealSense/gifs/realSenseSillhouttes.gif "Sillhouttes extracted with depth Thresholding ")

**Notes**

- Stereo cameras do not have an IR cut filter. So stereo is operational in only IR light.
- Provides good usb support and feedback. It says which usb type it is connected  to and continues to work at a lower quality when its connected to usb 2.0. 
- The 3D view provides dramatically less quality than the 2D view. (see above gifs)  
- Lists 1280x800 as an option, but it will not show any depth when that resolution is set.
- Also availble in an outdoor enclosure the Framos [D435e](https://www.framos.com/en/framos-depth-camera-d435e-camera-only-22806), but much more expensive. allows for POE over industrial ethernet connection M12. 

![Framos D435e](Assets/IntelRealSense/imgs/framos-D435e.png )
 
![Framos D435e](Assets/IntelRealSense/imgs/customCasing.png )
Custom casing produced by Antimodular for Speaking Willow project

#### Azure Kinect 

![Azure](Assets/azureKinect/azure_form.JPG )

Indoor Wide mode

![Indoor Wide mode Azure Kinect ](Assets/azureKinect/gifs/AKinect_inside_wide.gif "Indoor Wide mode Azure Kinect")

Indoor Narrow mode

![Indoor Narrow mode Azure Kinect ](Assets/azureKinect/gifs/AKinect_inside_narrow.gif "Indoor Narrow mode Azure Kinect")

Outdoor Wide mode 2.1M

![Outdoor Wide mode Azure Kinect ](Assets/azureKinect/gifs/AKinect_outside_wide.gif "Outdoor Wide mode Azure Kinect")

Outdoor Narrow mode 3.1M

![Outdoor Narrow mode Azure Kinect ](Assets/azureKinect/gifs/AKinect_outside_narrow.gif "Outdoor Narrow mode Azure Kinect")



**Notes**

- If it has something in the near field, far field drops/poorly affected. Example: Cannot be sitting in middle of table with table in view, needs to be on the edge of the table
- Provides significantly better range in the "binded" mode.
- The reported range is much smaller than what we observed in testing. In NFOV mode indoors it extended up to 11 meters, but the [specs](https://docs.microsoft.com/en-us/azure/Kinect-dk/hardware-specification) only report a range up to 5.46 meters in NFOV mode. 


#### Kinect v2

![kinect2](Assets/kinect2/kinect2_form.JPG )

Indoor 

![Indoor Kinect ](Assets/kinect2/gifs/kinect2_indoors.gif "Indoor Kinect")

Outdoor 2.4M

![Outdoor Kinect ](Assets/kinect2/gifs/kinect2_outdoors.gif "Outdoor Kinect")


**Notes**

- Discontinued support 
- A lot of harware accessories
- plug and play installation 

## Camera + Segmentation   

Overall the advantage of this technique is that it cuts out the work of manually cutting out the background through a region of interest and provides potentially useful additional information like the 3D skeleton, unique IDs for each person in the scene. It will also only mask people and will ignore all other backround objects. The disadvantages include: limited ranges, inability to track from certain angles, higher required specs to perform well. 

### Data

| Approach                        | Range M | Sillhoutte Quality (1-5 best) | Skeleton Quality (1-5) | Angle (1-5) |
|---------------------------------|---------|-------------------------------|------------------------|-------------|
| Azure Kinect+ body tracking SDK | 7       | 3                             | 5                      | 3           |
| BodyPix 2                       | 6.7     | 1                             | 0                      | 4           |
| Kinect v2 + body tracking SDK   | 4.2     | 0                             | 3                      | 2           |
| Oak-D + Segmentation     | --       | ---                          | ---                  | ---         |
| Nvidia Broadcast Engine    | --       | --                            | --                    | --          |
| Detectron    | --       | 5                            | --                    | --          |

### Footage + Notes


#### Intel RealSense + NuiTrack


Distance 

![Intel RealSense + NuiTrack Distance](Assets/nuitrack/gifs/nuitrack_distance.gif "Intel RealSense + NuiTrack")

Occlusion

![Intel RealSense + NuiTrack Occlusion ](Assets/nuitrack/gifs/nuitrack_occlusion.gif "Intel RealSense + NuiTrack Occlusion")

Angle

![Intel RealSense + NuiTrack Occlusion ](Assets/nuitrack/gifs/nuitrack_angle.gif "Intel RealSense + NuiTrack Occlusion")

**Notes**

- They threshold the depth data at 4M in the example. Is it possible to increase that threshold through their API?  
- As of writing, there is no support for [multiple sensors](https://community.nuitrack.com/t/adding-multiple-cameras-to-nuitrack/991/11). 

#### Azure Kinect + body Track SDK 

Distance 

![Azure Kinect + body Track SDK  Distance](Assets/azureTrack/gifs/azureTrack_distance.gif "Azure Kinect + body Track SDK ")

Occlusion

![Azure Kinect + body Track SDK  Occlusion ](Assets/azureTrack/gifs/azureTrack_occlusion.gif "Azure Kinect + body Track SDK Occlusion")

Angle

![Azure Kinect + body Track SDK  Angle ](Assets/azureTrack/gifs/azureTrack_angle.gif "Azure Kinect + body Track SDK Angle")


**Notes**

- Tracking range and persistence is impressive.
- Less false skeletons than earlier kinect.
- Example only available in NFOV mode and not available in wide mode. Tracking range would decrease in wide mode. 
- While the skeleton information is robust the silhouette segmentation is patchy.
- Requires high specs to run the tracking sdk. 

#### Kinect 2 + body Track SDK

Distance 

![Indoor Kinect Distance](Assets/kinect2/gifs/kinect2_distance.gif "Indoor Kinect Distance")

Occlusion 

![Indoor Kinect Occlusion](Assets/kinect2/gifs/kinect2_occulsion.gif "Indoor Kinect Occlusion")
 
Angle 

![Indoor Kinect Angle](Assets/kinect2/gifs/kinect2_angle.gif "Indoor Kinect Angle")

**Notes**

- No silhouette segmentation available. 
- frequent false positives.

#### Oak-D 
![Oak-D Image](Assets/oakD/oak-d.jpg "Oak-D")

![Oak-D Depth](Assets/oakD/gifs/oakD-Depth.gif "Oak-D Stereo Depth")

![Oak-D Depth](Assets/oakD/gifs/oakD-deeplabv3p.gif "deeplabv3p")


Angle 

![Oak-D Depth](Assets/oakD/gifs/oakD-deeplabv3p-overhead.gif "Oak-D From Overhead")

**Notes**


- See full testing [here](https://www.notion.so/Oak-D-Testing-9703b1a764e8483c8b381e1e4691a585)
- Limited FOV depending on the model used 
- Offloads processing to the device iself rather than on the computer 
- Many models available through openVINO
- Segmentation tested with deeplabv3p_person model


#### BodyPix 2

Multiperson RGB

![BodyPix Sample](Assets/bodyPix2/gifs/bodyPix-RGB-MultiPerson-translucent2.gif "BodyPix2 Sample")
ResNet50, internalResolution full, output stride 32. (full settings [here](Assets/bodyPix2/clips/bodyPix-RGB-MultiPerson-translucent2.mov))

Multiperson RGB Masked

![BodyPix Sample](Assets/bodyPix2/gifs/bodyPix-RGB-MultiPerson-opaque.gif "BodyPix2 Sample")
(full settings [here](Assets/bodyPix2/clips/bodyPix-RGB-MultiPerson-opaque.mov))

Multiperson IR 

![BodyPix Sample](Assets/bodyPix2/gifs/bodyPix-IR-MultiPerson-translucent.gif "BodyPix2 Sample")

(full settings [here](Assets/bodyPix2/clips/bodyPix-IR-MultiPerson-translucent.mov))
Simulate night conditions with IR illumination 

Multiperson IR Opaque

![BodyPix Sample](Assets/bodyPix2/gifs/bodyPix-IR-MultiPerson-opaque.gif "BodyPix2 Sample")

(full settings [here](Assets/bodyPix2/clips/bodyPix-IR-MultiPerson-opaque.mov))

Angle

![BodyPix Sample](Assets/bodyPix2/gifs/overheadBodyPix.gif "BodyPix Sample")

**Notes**

- Ran test on Windows 10 (3.6 GHz, 32GB of Ram, GeForce RTX 2080)
- Performed much better under with IR only light than the Nvidia Broadcast Engine
- Tested with Google's Coral USB Accelerator for running bodypix locally ([link to test](Assets/bodyPix2/gifs/coralReference4.gif)). As of writing this it was challenging to set up and [no automatic smoothing](https://github.com/google-coral/project-bodypix/issues/5) available. 

#### Nvidia Broadcast Engine

Multiperson RGB

![Nvidia Broadcast Engine Sample](Assets/NvidiaBroadcastEngine/gifs/nvidia-RGB-multiPerson2.gif "Nvidia Broadcast Engine Sample")

Multiperson RGB Masked 

![Nvidia Broadcast Engine Sample](Assets/NvidiaBroadcastEngine/gifs/nvidia-RGB-multiPerson-masked.gif "Nvidia Broadcast Engine Sample")

Multiperson IR

![Nvidia Broadcast Engine Sample](Assets/NvidiaBroadcastEngine/gifs/nvidia-IR-multiPerson.gif "Nvidia Broadcast Engine Sample")

Single person IR Masked

![Nvidia Broadcast Engine Sample](Assets/NvidiaBroadcastEngine/gifs/nvidia-IR-single-masked.gif "Nvidia Broadcast Engine Sample")

**Notes**

- Ran test on Windows 10 (3.6 GHz, 32GB of Ram, GeForce RTX 2080)
- Very easy to install and use when the very high specs are met.  
- The intended purpose is to mask out gamers as they are streaming. Definitely using this outside of its intended purpose- in IR light only and at a greater distance. 

### Detectron 

| rcnn                    | PointRend|
|---------------------------------|---------|
| ![detectron](Assets/detectron/imgs/rcnn-mask1.jpg )| ![detectron](Assets/detectron/imgs/pntRendResult1.jpg )|
| ![detectron](Assets/detectron/imgs/rcnn-mask2.jpg )| ![detectron](Assets/detectron/imgs/pntRendResult2.jpg )|
| ![detectron](Assets/detectron/imgs/rcnn-mask3.jpg )| ![detectron](Assets/detectron/imgs/pntRendResult3.jpg )|
| ![detectron](Assets/detectron/imgs/rcnn-mask4.jpg )| ![detectron](Assets/detectron/imgs/pntRendResult4.jpg )|
| ![detectron](Assets/detectron/imgs/rcnn-mask5.jpg )| ![detectron](Assets/detectron/imgs/pntRendResult5.jpg )|
| ![detectron](Assets/detectron/imgs/rcnn-mask6.jpg )| ![detectron](Assets/detectron/imgs/pntRendResult6.jpg )|   


## Other Possibilities  

This isn't an exhaustive list. Here are some of the other promising possibilities.

- [OpenCV BackgroundSubtractorMOG](https://docs.opencv.org/3.3.0/db/d5c/tutorial_py_bg_subtraction.html) - traditional rgb camera with no ML. Requires calibration when the scene changes. 
- [foreground extraction - FgSegNet_v2](https://github.com/lim-anggun/FgSegNet_v2) - ML approach with an RGB camera. Would need high specs for a good fps and resolution.
- [maskrcnn-benchmark](https://github.com/facebookresearch/maskrcnn-benchmark/issues/42) - ML approach on RGB camera. Only masks and not labels would be necessary. Looks like it has a max of 10 fps for realtime performance. 
- [VideoPose3D](https://github.com/facebookresearch/VideoPose3D) - Doesn't provide silhouettes and not intended for realtime. 
- [arkit IOS](https://developer.apple.com/documentation/arkit/arbody2d) - Only available in IOS
- [Detectron realtime](https://github.com/cedrickchee/realtime-detectron) - FPS is still low for realtime


