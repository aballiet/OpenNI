OpenNI (Version 1.5.4.0 - May 7th 2012) **modified to support C++ 11**
---------------------------------------

Website: http://www.primesense.com
Forum: http://groups.google.com/group/openni-dev
Wiki: http://wiki.openni.org

Binaries are available at:
http://www.openni.org/Downloads/OpenNIModules.aspx
(The "OpenNI Binaries" section)

Sources are available at:
https://github.com/OpenNI/OpenNI
or
https://github.com/OpenNI/OpenNI/tree/unstable
for unstable branch

# Checking requirements (SSE flags)

Compiler uses SSE3 flag parameter by default and thus if your device does not, you will to change this.

To know if your device supports SSE3 run :

``` bash
cat /proc/cpuinfo
```

Look at the row : flags
- If you find sse3 then you can directly proceed to the installation
- If you do not but find sse2, edit the file [Platform.x86](./Platform/Linux/Build/Common/Platform.x86) and transform `SSE_GENERATION = 3` into `SSE_GENERATION = 2`

> Note that if you need `SSE_GENERATION = 2`, you will have to do the same for the part: [Test your installation](<#Test your installation>)

# Installation

``` bash
cd
mkdir kinect cd ~/kinect
git clone https://github.com/aballiet/OpenNI.git
cd OpenNI
cd Platform/Linux/CreateRedist
chmod +x RedistMaker
./RedistMaker
cd ../Redist/OpenNI-Bin-Dev-Linux-[xxx] # where [xxx] is your architecture and release version
sudo sh install.sh
```

# Test your installation

Tthe Kinect sensor won't work out of the box with OpenNI. Avin2 has created a module that allows the Kinect Controller to work with OpenNI.

``` bash
cd ~/kinect
git clone https://github.com/avin2/SensorKinect
```

Copy [XnSensorDepthGenerator.cpp](./Resources/XnSensorDepthGenerator.cpp) and [XnSensorDepthGenerator.h](./Resources/XnSensorDepthGenerator.h) into SensorKinect/Source/XnDeviceSensorV2 :

``` bash
cp ./OpenNI/Resources/XnSensorDepthGenerator.h ./SensorKinect/Source/XnDeviceSensorV2/

cp ./OpenNI/Resources/XnSensorDepthGenerator.cpp ./SensorKinect/Source/XnDeviceSensorV2/
```

## Installation

``` bash
cd SensorKinect/Platform/Linux/Build
make && sudo make install
cd ../Redist/Sensor-Bin-Linux-[xxx] # where [xxx] is your architecture and release version
sudo sh install.sh
```

## NiViewer !!! 

``` bash
cd ~/kinect/OpenNI/Platform/Linux/Bin/xxx-Release
./NiViewer
```

You should now be able to see what your Kinect sees !

# Uninstall
``` bash
sudo ./install.sh -u
```