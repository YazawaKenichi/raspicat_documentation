# SSH でキャットにつなぐ（有線 LAN ）
```
source ~/.bashrc
ssh ubuntu@$ETHERNET_IP
```

# マッピングからナビゲーションまで

## IMU の立ち上げ方
LiDAR を先に刺してから IMU を刺す

Raspberry piで実行
terminal1で実行
```
ros2 run rt_usb_9axisimu_driver rt_usb_9axisimu_driver
```

terminal２で実行
```
ros2 lifecycle set rt_usb_9axisimu_driver configure
ros2 lifecycle set rt_usb_9axisimu_driver activate
```

## マップをとる
Raspberry Piで実行
```
ros2 launch raspicat raspicat.launch.py
```
```
ros2 service call /motor_power std_srvs/SetBool '{data: true}'
```
```
ros2 launch raspicat_bringup teleop.launch.py teleop:=joy
```
```
ros2 bag record -a
```

### 取得したrosbagをノートPCに移動(PC側)(無線Ver)
```
sudo scp -r ubuntu@192.168.12.1:~/取ったrosbagのディレクトリ名 ~/
```

#### USBで別のPCに

## マップ作成（別のPC）
```
ros2 launch raspicat_slam raspicat_slam_toolbox.launch.py
```
```
ros2 bag play -r 1 --clock 100 取ったrosbagのディレクトリ名
```
```
ros2 run nav2_map_server map_saver_cli -f ~/つけたいマップの名前
```

## マップ加工

USBでマップをナビゲーションをするPC持って来る

## マップを使う準備
ノートPCで実行
```
cd ~raspicat2/src/raspicat_slam_navigation
git switch feat/localization-and-navigation-map
```
マップを以下のディレクトリに
raspicat_slam/config/maps
以下の２つのマップの絶対パスを使用するマップのものに変更
ナビゲーションに使用するマップの絶対パス
自己位置推定に使用するマップの絶対パス

ナビゲーション
ノートPCで実行
```
cd ~/raspicat2
colcon build --packages-select raspicat_description emcl2 raspicat_setup_scripts raspicat_slam raspicat_speak2 raspicat_bringup raspicat_navigation raspicat raspicat_gazebo nav2_waypoint_follower nav2_rviz_plugins nav2_msgs raspimouse_msgs teleop_twist_joy
. install/setup.bash 
```

Raspberry Piで実行
```
ros2 launch raspicat raspicat.launch.py
```

ノートPCで実行
```
ros2 service call /motor_power std_srvs/SetBool '{data: true}'
ros2 launch raspicat_navigation raspicat_nav2.launch.py
```

