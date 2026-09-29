# 6. Launch 与工具链

ROS 2 不只是一个通信框架，它还提供了一整套开发和运行工具，用于启动进程、调试系统、记录数据、可视化状态和管理节点。

## 6.1 launch 机制

ROS 2 的 launch 功能允许你一次性启动多个节点、配置参数、设置环境变量、控制启动顺序和调试流程。

举例：

- 启动激光雷达驱动
- 启动定位模块
- 启动导航模块
- 启动 RViz

这些都可以放在一个 launch 文件中统一管理。

## 6.2 launch 文件的作用

常见作用包括：

- 启动多个 Node
- 配置参数
- 动态生成节点
- 延时启动
- 按顺序执行任务
- 测试系统启动行为

## 6.3 常见工具

### ros2

`ros2` 是 ROS 2 的命令行入口，支持：

- 节点管理
- topic 查看
- service 调用
- 参数查看
- bag 记录
- 节点列表

示例：

```bash
ros2 topic list
ros2 topic echo /chatter
ros2 node list
ros2 param list
```

### rviz2

rviz2 是 ROS 2 的可视化工具，通常用于：

- 显示点云
- 显示机器人模型
- 可视化 TF
- 观察传感器状态

### rqt

rqt 是 ROS 2 的图形化工具集合，适合：

- 监控网络状态
- 观察 topic / service / action
- 调试节点状态

### rosbag2

rosbag2 用于记录和回放 ROS 2 数据，用于：

- 采集测试数据
- 重放 sensor data
- 回归测试

## 6.4 常用命令

```bash
ros2 run <package> <node>
ros2 launch <package> <launch_file>
ros2 topic list
ros2 topic echo /topic_name
ros2 service list
ros2 param list
ros2 bag record /topic_name
```

## 6.5 为什么需要 launch

对于复杂系统而言，很难手动逐个启动节点。launch 提供了：

- 自动启动秩序
- 参数统一管理
- 便于调试和部署
- 便于多人协作维护

## 6.6 工具链与源码阅读关系

从源码角度看，工具链本质上是对 ROS 2、rclcpp、rmw、DDS 的上层运维层封装。更准确地说：

- ros2 提供命令入口
- launch 提供运行脚本入口
- bag 提供数据采集能力
- rviz 提供可视化能力

## 6.7 最优学习方式

建议先掌握：

- `ros2 run`
- `ros2 topic list`
- `ros2 node list`
- `ros2 topic echo`
- `ros2 launch`

然后再学习 rviz 和 rosbag。

## 6.8 一句话总结

ROS 2 的工具链让开发者能够更高效地启动节点、调试系统、可视化状态、记录数据，并把复杂 robot 系统组织成可维护的工作流。
