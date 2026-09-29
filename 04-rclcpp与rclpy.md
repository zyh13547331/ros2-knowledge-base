# 4. rclcpp 与 rclpy

ROS 2 提供了多种语言客户端库，其中最常见的是 C++ 的 rclcpp 和 Python 的 rclpy。它们都建立在底层的 rcl + rmw + DDS 之上，并为开发者提供统一的高层接口。

## 4.1 rclcpp 和 rclpy 的定位

- rclcpp：适合高性能、实时性要求更高、算法开发较重的 C++ 程序
- rclpy：适合脚本、原型、自动化控制和原型开发

两者的核心思路相同：

- Node
- Publisher / Subscriber
- Service / Client
- Action / Goal / Feedback / Result
- Timer
- Parameter
- Callback / Executor

## 4.2 rclcpp 的典型结构

rclcpp 中最典型的对象包括：

- rclcpp::Node
- rclcpp::Publisher
- rclcpp::Subscription
- rclcpp::Timer
- rclcpp::Client
- rclcpp::Service
- rclcpp::Parameter

### 创建节点

```cpp
#include "rclcpp/rclcpp.hpp"

class MyNode : public rclcpp::Node
{
public:
  MyNode() : Node("my_node")
  {
    RCLCPP_INFO(this->get_logger(), "Hello ROS 2!");
  }
};
```

### 创建 Publisher

```cpp
auto pub = this->create_publisher<std_msgs::msg::String>("chatter", 10);
```

### 创建 Subscriber

```cpp
auto sub = this->create_subscription<std_msgs::msg::String>(
  "chatter",
  10,
  [this](const std_msgs::msg::String::SharedPtr msg) {
    RCLCPP_INFO(this->get_logger(), "Received: '%s'", msg->data.c_str());
  });
```

### 创建 Timer

```cpp
this->create_wall_timer(std::chrono::milliseconds(500), [this]() {
  auto msg = std_msgs::msg::String();
  msg.data = "hello";
  pub_->publish(msg);
});
```

## 4.3 rclpy 的典型结构

rclpy 也有对应的 Python 结构：

- rclpy.init()
- Node
- Publisher
- Subscription
- Timer
- Service / Client

### 创建节点

```python
import rclpy
from rclpy.node import Node

class MyNode(Node):
    def __init__(self):
        super().__init__('my_node')
        self.get_logger().info('Hello ROS 2!')
```

### 创建 Publisher

```python
self.pub = self.create_publisher(String, 'chatter', 10)
```

### 创建 Subscriber

```python
self.sub = self.create_subscription(String, 'chatter', self.callback, 10)
```

### 创建 Timer

```python
self.timer = self.create_timer(0.5, self.timer_callback)
```

## 4.4 共同设计思想

rclcpp 和 rclpy 的设计理念一致：

- 通过 Node 管理生命周期
- 通过 callback 处理消息
- 通过 executor 调度任务
- 通过 ROS 2 运行时统一调度所有事件

## 4.5 Executor（执行器）

Executor 是 ROS 2 的事件循环和调度器，负责：

- 回调消息处理
- 处理 timer
- 执行 service client
- 调度 action 回调

常见执行器：

- SingleThreadedExecutor
- MultiThreadedExecutor
- StaticSingleThreadedExecutor

其本质上就是：

- 让 ROS 2 系统在运行时持续分发回调事件

## 4.6 语言选择建议

### 选择 rclcpp

适合：

- 机器人底层控制
- 高性能场景
- C++ 编译器较成熟的项目
- 需要跨平台和实时控制

### 选择 rclpy

适合：

- 算法原型
- 脚本逻辑
- 研究和尝试性开发
- 快速验证

## 4.7 二者的关系

rclcpp 和 rclpy 都是 ROS 2 的语言绑定层，底层都依赖：

- rcl（C 层接口）
- rmw（中间件适配）
- DDS（实际通信）

因此它们在逻辑上是同一套 ROS 2 语义，不是两个完全不同的系统。

## 4.8 学习顺序建议

最合理的学习路径：

1. 先学习 rclcpp 的 Node / Publisher / Subscriber / Timer
2. 再学习 rclpy 的同类概念
3. 然后理解 executor、callback、QoS
4. 最后深入 rmw / DDS / rcl

## 4.9 一句话总结

rclcpp 和 rclpy 是 ROS 2 语言层接口，分别为 C++ 和 Python 用户提供统一的 Node、Publisher、Subscriber、Service、Action 和 Timer 能力，而底层仍然依赖 rcl + rmw + DDS 来完成实际通信。
