# ROS 2 学习知识库

这是一个面向 ROS 2 初学者和源码阅读者整理的知识库，目标是帮助你从“知道 ROS 2 是什么”逐步走到“能写 ROS 2 程序、能看 ROS 2 源码、能做实际项目”。

## 适合谁

- 想学习 ROS 2 的新手
- 想看 ROS 2 官方源码的人
- 想做机器人/自动化项目的人
- 想理解 ROS 2 架构、DDS、QoS 和通信机制的人

## 知识库结构

- [01-ROS2基础概念.md](./01-ROS2基础概念.md)
- [02-ROS2系统架构.md](./02-ROS2系统架构.md)
- [03-通信机制与DDS.md](./03-通信机制与DDS.md)
- [04-rclcpp与rclpy.md](./04-rclcpp与rclpy.md)
- [05-QoS与实时性.md](./05-QoS与实时性.md)
- [06-Launch与工具链.md](./06-Launch与工具链.md)
- [07-调试与排错.md](./07-调试与排错.md)
- [08-最佳实践.md](./08-最佳实践.md)
- [09-源码阅读路径.md](./09-源码阅读路径.md)
- [10-示例工程.md](./10-示例工程.md)
- [QUICK-START.md](./QUICK-START.md)

## examples 目录

仓库里提供了可直接运行的最小示例工程：

- [examples/01-minimal-publisher-subscriber](./examples/01-minimal-publisher-subscriber)
- [examples/02-service-client](./examples/02-service-client)
- [examples/03-timer-callback](./examples/03-timer-callback)
- [examples/04-parameter-management](./examples/04-parameter-management)
- [examples/05-multiple-nodes](./examples/05-multiple-nodes)

## 学习路线

推荐顺序：

1. 先看 README 和 QUICK-START
2. 学习 01 基础概念
3. 学习 02 系统架构
4. 学习 03 通信机制与 DDS
5. 学习 04 rclcpp 与 rclpy
6. 学习 05 QoS 与实时性
7. 跑示例工程
8. 阅读 09 源码阅读路径
9. 最后回到 08 最佳实践和 07 调试排错

## 学习目标

通过这份知识库，你应该能够：

- 解释 ROS 2 的核心概念
- 理解 Node、Topic、Service、Action、Parameter 的差异
- 理解 ROS 2 分层架构：RCL、RMW、DDS
- 理解 rclcpp / rclpy 的作用和关系
- 掌握 QoS 的核心思想
- 能运行最小 ROS 2 示例工程
- 能看懂 ROS 2 官方源码中的关键调用链

## 官方资源

- ROS 2 官方文档: https://docs.ros.org/
- ROS 2 设计文档: https://github.com/ros2/design
- ROS 2 官方示例: https://github.com/ros2/examples
- ROS 2 主仓库: https://github.com/ros2/ros2
- rclcpp: https://github.com/ros2/rclcpp
- rclpy: https://github.com/ros2/rclpy
- rmw: https://github.com/ros2/rmw

## 一句话总结

ROS 2 的本质是：用分布式消息通信与服务动作模型，连接不同节点，用 DDS 作为底层通信基础，用 RCL/RMW 把这些能力封装成统一 API，最终让机器人和自动化系统在多个进程、多个节点、多个设备之间高效协作。

## 适合你当前阶段的建议

如果你目标是“先真正能理解并运行 ROS 2”，建议按这个顺序：

- 先看 QUICK-START.md
- 再看 01 和 02
- 跑 examples/01-minimal-publisher-subscriber
- 然后看 03 和 04
- 最后再读 09 源码阅读路径

不要一开始就死磕 DDS 实现细节，先建立整体认知，再往下读源码。