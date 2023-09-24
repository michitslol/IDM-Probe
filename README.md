# IDM scanner

#### 介绍
idm scanner 上位机python代码
修改自beacon

#### 软件架构
软件架构说明

#### 使用说明
``` 
在用户目录下执行git clone https://gitee.com/NBTP/IDM.git 下载程序包

执行chmod +x IDM/install.sh
然后执行IDM/install.sh进行安装
这一步会自动把脚本创建一个链接放到klipper/klipper/extra目录下
然后
[idm]
serial:/dev/serial/by-id/usb-IDM_614e_473431383817584A-if00
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
将这段配置放进printer.cfg并将serial修改为你查询到的idm的串口号
在配置里再加入
[force_move]
enable_force_move: true
方便校准，校准全部结束后可删除

之后把[probe]模块删除
并将z限位修改为probe:z_virtual_endstop
还需要设置
[safe_z_home]
home_xy_position: 【你的x轴中心坐标】,【你的y轴中心坐标】
z_hop: 10
记得设置[bed_mesh]不然会报错

重启之后将徒手热端移动到中间并将喷嘴贴到平台上
输入SET_KINEMATIC_POSITION x=【平台中心x坐标】 y=【平台中心y轴坐标】 z=0
之后执行idm_calibrate的指令
点击-0.1的偏移后确认，会自动进行校准
在控制台输入idm并按tab键可以看到所有支持的指令
```

#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request


#### 特技

1.  使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2.  Gitee 官方博客 [blog.gitee.com](https://blog.gitee.com)
3.  你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解 Gitee 上的优秀开源项目
4.  [GVP](https://gitee.com/gvp) 全称是 Gitee 最有价值开源项目，是综合评定出的优秀开源项目
5.  Gitee 官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6.  Gitee 封面人物是一档用来展示 Gitee 会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)
