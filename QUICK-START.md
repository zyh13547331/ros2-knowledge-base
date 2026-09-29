# 快速开始指南

这份指南将一步步教你创建并运行所有 ROS 2 示例工程。

## 环境准备

确保你已经安装了 ROS 2。可以参考[官方安装指南](https://docs.ros.org/en/rolling/Installation.html)。

验证安装：

```bash
ros2 --version
```

## 1. Publisher 和 Subscriber 示例

这是最基础的 ROS 2 通信模式。

### 创建工作空间

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
```

### 创建 package

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake minimal_pub_sub --dependencies rclcpp std_msgs
cd minimal_pub_sub
```

### 复制源文件

从仓库的 `examples/01-minimal-publisher-subscriber/` 目录复制：

- `CMakeLists.txt` → `~/ros2_ws/src/minimal_pub_sub/CMakeLists.txt`
- `package.xml` → `~/ros2_ws/src/minimal_pub_sub/package.xml`
- `src/talker.cpp` → `~/ros2_ws/src/minimal_pub_sub/src/talker.cpp`
- `src/listener.cpp` → `~/ros2_ws/src/minimal_pub_sub/src/listener.cpp`

### 编译

```bash
cd ~/ros2_ws
colcon build --packages-select minimal_pub_sub
```

### 运行

**终端 1：运行 Talker**

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 run minimal_pub_sub talker
```

你会看到输出：

```
[INFO] [minimal_pub_sub.talker]: Talker node started
[INFO] [minimal_pub_sub.talker]: Publishing: 'Hello from ROS 2 - 0'
[INFO] [minimal_pub_sub.talker]: Publishing: 'Hello from ROS 2 - 1'
...
```

**终端 2：运行 Listener**

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 run minimal_pub_sub listener
```

你会看到输出：

```
[INFO] [minimal_pub_sub.listener]: Listener node started
[INFO] [minimal_pub_sub.listener]: I heard: 'Hello from ROS 2 - 0'
[INFO] [minimal_pub_sub.listener]: I heard: 'Hello from ROS 2 - 1'
...
```

**终端 3：查看 Topic 信息**

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 topic list
ros2 topic echo /chatter
ros2 topic hz /chatter
```

## 2. Service 和 Client 示例

这个示例演示如何使用 Service 进行请求/响应通信。

### 创建 package

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake minimal_service --dependencies rclcpp example_interfaces
```

### 复制文件

从 `examples/02-service-client/` 目录复制所有文件。

### 编译

```bash
cd ~/ros2_ws
colcon build --packages-select minimal_service
```

### 运行

**终端 1：运行 Service Server**

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 run minimal_service server
```

输出：

```
[INFO] [minimal_service.add_two_ints_server]: Service server started
```

**终端 2：运行 Client**

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 run minimal_service client
```

输出：

```
[INFO] [minimal_service.add_two_ints_client]: Sending request: a=3 b=4
[INFO] [minimal_service.add_two_ints_client]: Sum: 7
```

## 3. Timer 和 Callback 示例

演示定时器的使用。

### 创建 package

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake minimal_timer --dependencies rclcpp
```

### 复制文件

从 `examples/03-timer-callback/` 目录复制所有文件。

### 编译

```bash
cd ~/ros2_ws
colcon build --packages-select minimal_timer
```

### 运行

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 run minimal_timer timer_node
```

输出：

```
[INFO] [minimal_timer.timer_node]: Timer node started
[INFO] [minimal_timer.timer_node]: Timer callback called 1 times
[INFO] [minimal_timer.timer_node]: Timer callback called 2 times
...
```

## 4. Parameter 参数管理示例

演示参数的配置和动态修改。

### 创建 package

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake minimal_parameter --dependencies rclcpp
```

### 复制文件

从 `examples/04-parameter-management/` 目录复制所有文件。

### 编译

```bash
cd ~/ros2_ws
colcon build --packages-select minimal_parameter
```

### 运行

**终端 1：运行节点**

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 run minimal_parameter param_node
```

输出：

```
[INFO] [minimal_parameter.parameter_node]: Parameter node started with: string=default_value, int=42, double=3.14
```

**终端 2：查看和修改参数**

```bash
cd ~/ros2_ws
source install/setup.bash

# 查看所有参数
ros2 param list

# 查看参数值
ros2 param get /parameter_node my_string
ros2 param get /parameter_node my_int

# 修改参数值
ros2 param set /parameter_node my_string "new_value"
ros2 param set /parameter_node my_int 100
```

在终端 1 会看到参数变更的日志。

## 5. 多节点协作示例

演示多个节点之间的通信。

### 创建 package

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake minimal_multi_node --dependencies rclcpp std_msgs launch_ros launch
```

### 复制文件

从 `examples/05-multiple-nodes/` 目录复制所有文件。

### 编译

```bash
cd ~/ros2_ws
colcon build --packages-select minimal_multi_node
```

### 使用 Launch 文件运行

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 launch minimal_multi_node demo.launch.py
```

输出：

```
[node_a-1] [INFO] [minimal_multi_node.node_a]: Node A started
[node_b-1] [INFO] [minimal_multi_node.node_b]: Node B started
[node_a-1] [INFO] [minimal_multi_node.node_a]: Node A publishing: 'Hello from Node A'
[node_b-1] [INFO] [minimal_multi_node.node_b]: Node B publishing: 'Hello from Node B'
[node_a-1] [INFO] [minimal_multi_node.node_a]: Node A received: 'Hello from Node B'
[node_b-1] [INFO] [minimal_multi_node.node_b]: Node B received: 'Hello from Node A'
```

## 常用 ROS 2 命令

```bash
# 列出所有节点
ros2 node list

# 查看节点详细信息
ros2 node info /node_name

# 列出所有 topic
ros2 topic list

# 查看 topic 详细信息
ros2 topic info /topic_name

# 监听 topic 消息
ros2 topic echo /topic_name

# 查看 topic 发布频率
ros2 topic hz /topic_name

# 列出所有参数
ros2 param list

# 查看参数值
ros2 param get /node_name parameter_name

# 设置参数值
ros2 param set /node_name parameter_name value

# 列出所有服务
ros2 service list

# 调用服务
ros2 service call /service_name ServiceType '{"field": value}'

# 查看日志等级
ros2 run package_name executable --ros-args --log-level info
```

## 编译和运行问题排查

### 问题：找不到 package

```bash
# 确保已 source 工作空间
source ~/ros2_ws/install/setup.bash

# 重新编译
colcon build
```

### 问题：依赖未找到

```bash
# 安装所有依赖
rosdep install --from-paths src --ignore-src -r -y

# 重新编译
colcon build
```

### 问题：编译失败

```bash
# 清除编译结果后重新编译
colcon build --packages-select package_name --cmake-args -DCMAKE_BUILD_TYPE=Debug
```

### 问题：节点无法启动

```bash
# 检查节点是否存在
ros2 run package_name --help

# 查看节点日志
ros2 run package_name executable --ros-args --log-level debug
```

## 下一步

1. 运行所有示例，理解每个示例的工作原理
2. 阅读对应的知识库章节，加深理解
3. 修改示例代码，尝试不同的参数和配置
4. 查看官方 ROS 2 源码，了解底层实现
5. 创建自己的第一个 ROS 2 工程

## 推荐阅读顺序

1. **QUICK-START.md** - 快速上手（本文件）
2. **01-ROS2基础概念.md** - 理解核心概念
3. **02-ROS2系统架构.md** - 理解分层架构
4. **03-通信机制与DDS.md** - 深入通信原理
5. **04-rclcpp与rclpy.md** - 学习 API 使用
6. **05-QoS与实时性.md** - 配置通信质量
7. **09-源码阅读路径.md** - 阅读源码指引
8. **08-最佳实践.md** - 工程最佳实践

## 常见问题

**Q: 为什么我的 Talker 和 Listener 无法通信？**

A: 检查以下几点：
- 确保两个节点都在运行
- 检查 topic 名是否一致
- 检查 QoS 配置是否兼容
- 查看节点日志是否有错误

**Q: 如何在一个节点中同时订阅多个 topic？**

A: 在构造函数中多次调用 `create_subscription`：

```cpp
sub1_ = this->create_subscription<Type1>("topic1", 10, callback1);
sub2_ = this->create_subscription<Type2>("topic2", 10, callback2);
```

**Q: 如何动态创建和销毁节点？**

A: 虽然不推荐，但可以使用 `std::make_shared` 和智能指针来管理节点的生命周期。

**Q: ROS 2 支持跨机器通信吗？**

A: 支持。只要机器在同一个网络上，ROS 2 会自动发现其他机器上的节点。确保 DDS 能够正确配置即可。

## 获取帮助

- 官方文档：https://docs.ros.org/
- ROS Discourse：https://discourse.ros.org/
- GitHub Issues：https://github.com/ros2/ros2/issues
