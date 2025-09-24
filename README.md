# roscpp_test

### package 제작 방법
- ros2 pkg create --build-type ament_cmake --node-name <노드이름> <패키지이름>

### ros 실행 방법
기본 세팅
```
source /opt/ros/jazzy/setup.bash
colcon build
source install/setup.bash
```

터미널 실행
```
ros2 run turtlesim turtlesim_node
ros2 run my_first_package_cpp my_subscription_cpp 
ros2 run my_first_package_cpp my_publisher_cpp 
```