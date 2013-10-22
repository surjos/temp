#### Razor AHRS v1.4.2

Updated firmware to be Arduino 1.x compatible and sketches to be Processing 2.x compatible.
Added ability to read plain sensor data of all 9 axes to Android library.
Fixed namespace issues in C++ library.

#### Moved to Github

New home of Razor AHRS is [github.com/ptrbrtz/razor-9dof-ahrs](https://github.com/ptrbrtz/razor-9dof-ahrs)

#### Razor AHRS v1.4.1

Additionally to magnetometer hard iron error compensation, Razor AHRS now also supports soft iron error compensation. Both compensations only work in the case of the hard/soft iron moving with the sensor - meaning not changing it's position relative to the sensors. Calibration is still static: it's done once and then being hardcoded into the firmware. Have a look at the new tutorial section about extended magnetometer calibration.

New output modes allow to read raw or calibrated direct sensor values on all 9 axes - very useful if you want to mess with sensor data directly. The C++ code was extended to be able to read data in these new modes, too. The Android lib will be updated soon.

#### C++ library BUGFIX

Just updated the v1.4.0 C++ library to fix a bug where reading from Serial Ports would fail on Linux. It seems on (some) Linux distributions when there is no data available on the port, non-blocking read() (using O_NDELAY) would return -1 with errno set to EAGAIN, while on Mac OS X read() would just return 0.

#### Razor AHRS v1.4.0 BUGFIX

Added an updated version of the v1.4.0 firmware on the files page. It fixes a sensor reading bug that was introduced in the original v1.4.0 release.  
You should redo the sensor calibration for the magnetometer and the gyroscope!  
Many thanks to Masafumi Miwa for finding and reporting the bug!

#### Razor AHRS v1.4.0

Razor AHRS now also supports SparkFun 9DOF Sensor Stick versions SEN-10183, SEN-10321 and SEN-10724.

#### Razor AHRS v1.3.3

Added a library to interface the Razor AHRS using Android devices. It does all I/O in a background thread and forwards incoming data to a listener in the main thread.  
An example project on how to use the lib is included.  

Also the synching mechanism was extended. Now an ID is sent with the synch request and will be returned in the synch response. That way it's possible to tell apart different synchs.  
Libraries and firmware from this release are not compatible with older releases.

#### Razor AHRS v1.3.2

Recently Arduino 1.0 was released and brought some changes.  
The Razor AHRS Firmware now compiles with Arduino 1.x as well as previous versions.

#### Added C++ library for Mac OSX / Unix / Linux

Added an easy to use C++ library to read data from the Razor. It does all I/O in a background thread and forwards incoming data using callbacks.  
Example code on how to use the lib is also included.  

#### Razor AHRS v1.3.1

Major changes:
* Fixed a bug where firmware would not compile if OUTPUT__HAS_RN_BLUETOOTH was enabled.
* Added initialization of rotation matrix at start-up based on first (unfiltered) sensor readings. That means now yaw/pitch/roll output is correct right after boot - before it took one or two seconds to converge. This is particularly useful if the tracker is auto-reset upon every serial connect (occurring when using USB with DTR pin connected, see Tutorial).
* Adjusted gyro settings, so it should be more accurate now.