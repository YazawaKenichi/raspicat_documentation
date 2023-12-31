# 矢澤用ドキュメント

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

