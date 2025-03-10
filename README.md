# Pepperl+Fuchs SmartRunner Explorer Driver

This is the documentation of a driver for the Pepperl+Fuchs SmartRunner Explorer. This driver
The driver has a ROS-Node interface to the Robot Operating System (<http://www.ros.org>).


## Sensor information

The following Pepperl+Fuchs sensors are supported by this ROS driver.

### SmartRunner 3-D Explorer
The SmartRunner Explorer generates high-precision 3-D point cloud images in addition to 2-D images. 
It is optionally available with stereo vision technology or time-of-flight (ToF) technology. 
As a raw data sensor, the vision sensor is suitable for a wide variety of applications.

Official Website: https://www.pepperl-fuchs.com/global/en/smartrunner_3-d.htm

Datasheet (en): https://files.pepperl-fuchs.com/webcat/navi/productInfo/doct/tdoct7242a_eng.pdf

### SmartRunner Explorer

The SmartRunner Explorer is based on the innovative SmartRunner technology and outputs both height profiles and area 
images. SmartRunner technology combines the light-sectioning method for acquiring height profiles with the acquisition 
of area images via the integrated area illumination. In the light section method, a laser line is projected onto an 
object. This is captured at a specific angle by a camera. A height profile is then created using the triangulation 
principle. This laser technology enables reliable height profile recording on different surfaces.

Official Website: https://www.pepperl-fuchs.com/global/en/classid_9864.htm

Datasheet (en): https://files.pepperl-fuchs.com/webcat/navi/productInfo/pds/284586-100009_eng.pdf

## Usage with ROS
The ROS package `smartrunner_driver` consists of the driver library and a node named `smartrunner_node`.


#### Supported platforms:
- Ubuntu 20.04 / ROS Noetic
- Ubuntu 18.04 / ROS Melodic

#### Published topics
The following standard ROS messages are supported. The messages contain the measured data.

- `scan` (`sensor_msgs/PointCloud`)
- `scan` (`sensor_msgs/PointCloud2`)

#### Parameters

- `frame_id` - The frame-ID in the header of the published `sensor_msgs/PointCloud` messages
- `scanner_ip` - IP address or hostname of the sensor
- `message_type` - The type of the PointCloud-Message (PointCloud or PointCloud2)

#### Installation guide
1. Create a ROS workspace (http://wiki.ros.org/catkin/Tutorials/create_a_workspace) (e.g. in `<home>/catkin_ws`)
2. Clone the repository in the src folder of your ROS workspace.
```git clone https://github.com/PepperlFuchs/pf_smartrunner_ros_driver.git```
3. Download the library from the Pepperl+Fuchs site.
   (https://www.pepperl-fuchs.com/global/en/classid_9866.htm?view=productdetails&prodid=117291#software)
4. Unzip the downloaded file and copy the folder "VsxSdk" in to the folder:  
```<home>/catkin_ws/src/pf_smartrunner_ros_driver/smartrunner_driver/lib/```<br/>Change directory to <br/>```<home>/catkin_ws/src/pf_smartrunner_ros_driver/smartrunner_driver/lib/VsxSdk/C/lib/linux-x64/``` and call <br/>```ln -s PF.VsxProtocolDriver.WrapperNE.so libPF.VsxProtocolDriver.WrapperNE.so```.
4. Install .NET SDK.
   (https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-2004)
5. Change to the workspace directory.  
```<home>/catkin_ws/```
6. Run the command.   
```source devel/setup.bash```
7. Start the compilation.  
```catkin_make install```

#### Launch the driver
1. Set the IP-Address of the sensor, the message type and the sensor parameter in:  
```<home>/catkin_ws/src/pf_smartrunner_ros_driver/smartrunner_driver/launch/smartrunner.launch```  
2. Run the command:  
```roslaunch pepperl_fuchs_smartrunner smartrunner.launch```  
3. This starts `RViz` (http://wiki.ros.org/rviz) and the driver.
4. The measure points coming from the sensor are shown in the `RViz` window.


