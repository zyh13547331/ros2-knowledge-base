# ROS 2 知识库

这是一个面向 ROS 2 初学者和源码阅读者的知识库，覆盖 ROS 2 的核心概念、架构、通信机制、API、工具链，以及源码学习路线。

## 目录

- [1. ROS 2 基础概念](./01-ROS2基础概念.md)
- [2. ROS 2 系统架构](./02-ROS2系统架构.md)
- [3. 通信机制与 DDS](./03-通信机制与DDS.md)
- [4. rclcpp 与 rclpy](./04-rclcpp与rclpy.md)
- [5. QoS 与实时性](./05-QoS与实时性.md)
- [6. Launch 与工具链](./06-Launch与工具链.md)
- [7. 调试与排错](./07-调试与排错.md)
- [8. 最佳实践](./08-最佳实践.md)
- [9. 源码阅读路径](./09-源码阅读路径.md)
- [10. 示例工程](./10-示例工程.md)

## 项目目标

本知识库的目的不是记住所有 ROS 2 API，而是帮助你建立以下几个关键认知：

1. ROS 2 是什么：一个用于机器人和自动化系统的通信框架。
2. ROS 2 怎么工作：由节点、话题、服务、动作、参数等组成。
3. ROS 2 的底层结构：RMW、DDS、RCL、rclcpp/rclpy 分层设计。
4. 为什么 ROS 2 适合机器人系统：分布式、实时、跨平台、可扩展。
5. 如何阅读源码：从示例开始，逐层往下读到 DDS 和通信层。

## 学习建议

- 先学概念，再看源码。
- 先看 examples，再读 rclcpp。
- 先理解 Publisher/Subscriber，再理解 Service/Action/Parameter。
- 不要一开始就追底层 DDS 细节，先建立整体认识。
- 阅读源码时，建议按“调用链”顺序理解：Node -> Publisher -> RCL -> RMW -> DDS。

## 推荐阅读顺序

1. 先看 [01-ROS2基础概念.md]
2. 再看 [02-ROS2系统架构.md]
3. 然后看 [03-通信机制与DDS.md]
4. 最后阅读 [04-rclcpp与rclpy.md] 和 [09-源码阅读路径.md]

## 参考资源

- ROS 2 官方文档: https://docs.ros.org/
- ROS 2 设计文档: https://github.com/ros2/design
- ROS 2 官方示例: https://github.com/ros2/examples
- ROS 2 主仓库: https://github.com/ros2/ros2
- rclcpp 仓库: https://github.com/ros2/rclcpp
- rclpy 仓库: https://github.com/ros2/rclpy
- rmw 仓库: https://github.com/ros2/rmw

## 一句话概括

ROS 2 是基于 DDS 的分布式机器人软件开发框架，核心思想是“节点之间通过消息/服务/动作通信”，并通过 RMW/RCL 把这些抽象映射到底层中间件。

