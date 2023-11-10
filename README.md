NOTE: THIS IS  1 to 1 TRANSLATE FROM CHINESE FROM THE OFFICIAL MANUAL

#IDM scanner

#### introduce
idm scanner host computer python code
Modified from beacon

#### Software Architecture
Software architecture description

#### Instructions for use
```
To ensure accuracy, please install so that the top surface of the sensor coil plate is lower than the bottom surface of the heating block as much as possible.


Execute git clone https://gitee.com/NBTP/IDM.git in the user directory to download the package

Execute chmod +x IDM/install.sh
Then execute IDM/install.sh to install
This step will automatically create a link to the script and place it in the klipper/klipper/extra directory.

[idm]
serial:
#canbus_uuid:
#   Path to the serial port for the idm device. Typically has the form
#   /dev/serial/by-id/usb-idm_idm_...
speed: 40.
#   Z probing dive speed.
lift_speed: 5.
#   Z probing lift speed.
backlash_comp: 0.5
#   Backlash compensation distance for removing Z backlash before measuring
#   the sensor response.
x_offset: 0.
#   X offset of idm from the nozzle.
y_offset: 21.1
#   Y offset of idm from the nozzle.
trigger_distance: 2.
#   idm trigger distance for homing.
trigger_dive_threshold: 1.5
#   Threshold for range vs dive mode probing. Beyond `trigger_distance +
#   trigger_dive_threshold` a dive will be used.
trigger_hysteresis: 0.006
#   Hysteresis on trigger threshold for untriggering, as a percentage of the
#   trigger threshold.
cal_nozzle_z: 0.1
#   Expected nozzle offset after completing manual Z offset calibration.
cal_floor: 0.1
#   Minimum z bound on sensor response measurement.
cal_ceil:5.
#   Maximum z bound on sensor response measurement.
cal_speed: 1.0
#   Speed while measuring response curve.
cal_move_speed: 10.
#   Speed while moving to position for response curve measurement.
default_model_name: default
#   Name of default idm model to load.
mesh_main_direction: x
#   Primary travel direction during mesh measurement.
#mesh_overscan: -1
#   Distance to use for direction changes at mesh line ends. Omit this setting
#   and a default will be calculated from line spacing and available travel.
mesh_cluster_size: 1
#   Radius of mesh grid point clusters.
mesh_runs: 2
#   Number of passes to make during mesh scan.
Please pay attention to the x y direction offset in the adjustment configuration. Make sure that during the calibration process, the nozzle will move the coil to the xy position of the original nozzle.
Put this configuration into printer.cfg and change serial to the serial number of the idm you queried.
For the can version, use the regular query method to search for the uuid of can and fill it in.
Add it to the configuration
[force_move]
enable_force_move: true
Convenient for calibration and can be deleted after all calibrations are completed

Then delete the [probe] module
And modify the z limit to probe:z_virtual_endstop
Still need to set
[safe_z_home]
home_xy_position: [Your x-axis center coordinate], [Your y-axis center coordinate]
z_hop: 10
[Your x-axis center coordinate], [Your y-axis center coordinate]

After restarting, move the hot end to the middle and attach the nozzle to the platform with your bare hands
Input SET_KINEMATIC_POSITION x=[x-coordinate of platform center] y=[y-axis coordinate of platform center] z=0
Then execute the idm_calibrate command
Click on the offset of -0.1 to confirm, and calibration will be performed automatically.
Enter idm in the console and press the tab key to see all supported commands.

Lowering the horizontal_z_move in z_tilt or quad_gantry_level below trigger_distance + trigger_dive_threshold (default is 3) can put the leveling into high-speed mode. If it is too low, you can raise the trigger_dive_threshold appropriately so that horizontal_z_move can be raised higher.


For versions that include an accelerometer (lis2dw), you can enable the accelerometer by adding the following to the configuration:
[lis2dw]
cs_pin: idm:PA3
spi_bus: spi1

[resonance_tester]
accel_chip: lis2dw
probe_points:
    125, 125, 20  #Set here is the coordinates of the nozzle when you perform resonance measurement
```


#### Participate and contribute

1. Fork this warehouse
2. Create a new Feat_xxx branch
3. Submit code
4. Create a new Pull Request


#### Stunts

1. Use Readme\_XXX.md to support different languages, such as Readme\_en.md, Readme\_zh.md
2. Gitee official blog [blog.gitee.com](https://blog.gitee.com)
3. You can learn about excellent open source projects on Gitee at [https://gitee.com/explore](https://gitee.com/explore)
4. [GVP](https://gitee.com/gvp) The full name is Gitee’s most valuable open source project, which is an excellent open source project evaluated comprehensively.
5. Official user manual provided by Gitee [https://gitee.com/help](https://gitee.com/help)
6. Gitee Cover Character is a column used to showcase the style of Gitee members [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)
