# 矢澤用ドキュメント

## SSH
``` cmd
ssh ubuntu@$ETHERNET_IP
```

## ビルド
``` bash
cd ~/raspicat2
colcon build --packages-select raspicat_description emcl2 raspicat_setup_scripts raspicat_slam raspicat_speak2 raspicat_bringup raspicat_navigation raspicat raspicat_gazebo nav2_waypoint_follower nav2_rviz_plugins nav2_msgs raspimouse_msgs teleop_twist_joy
. install/setup.bash
```

## 実行
``` bash
ros2 launch raspicat_gazebo raspicat_with_iscas_museum.launch.py
```
``` bash
ros2 service call /motor_power std_srvs/SetBool '{data: true}'
```
``` bash
ros2 launch raspicat_navigation raspicat_nav2.launch.py map:=$HOME/map.yaml
```

# 棒状の器具実験

## micro-ROS Agent
``` cmd
source ~/yazawa/.bashrc
ros2 run micro_ros_agent micro_ros_agent serial -b 115200 --dev /dev/ttyACM0 -v6
```

## raspicat.launch
``` cmd
source ~/yazawa/.bashrc
ros2 launch raspicat raspicat.launch.py
```

## teleop
``` cmd
source ~/yazawa/.bashrc
ros2 launch raspicat_bringup teleop.launch.py teleop:=joy
```

## motor on
``` cmd
source ~/yazawa/.bashrc
ros2 service call /motor_power std_srvs/SetBool '{data: true}'
```

## bag
``` cmd
source ~/yazawa/.bashrc
ros2 bag record -a
```


