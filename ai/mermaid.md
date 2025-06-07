# Mermaid 图表示例

## 1. 流程图 (Flowchart)

### 基本语法

```mermaid
graph TD
    A[开始] --> B{判断条件}
    B -->|是| C[处理1]
    B -->|否| D[处理2]
    C --> E[结束]
    D --> E
```

awdawdaw
awdwadaw

awdawdwa
awdaw

### 实际应用：用户登录流程

```mermaid
graph LR
    A[用户输入] --> B{验证信息}
    B -->|成功| C[登录成功]
    B -->|失败| D[显示错误]
    D --> A
    C --> E[进入系统]
```

## 2. 时序图 (Sequence Diagram)

### 基本语法

```mermaid
sequenceDiagram
    participant A as 客户端
    participant B as 服务器
    A->>B: 请求数据
    B-->>A: 返回数据
```

### 实际应用：支付流程

```mermaid
sequenceDiagram
    participant U as 用户
    participant S as 商城
    participant P as 支付系统
    participant B as 银行
    U->>S: 提交订单
    S->>P: 创建支付请求
    P->>B: 扣款请求
    B-->>P: 扣款结果
    P-->>S: 支付结果
    S-->>U: 订单确认
```

## 3. 甘特图 (Gantt Chart)

### 基本语法

```mermaid
gantt
    title 项目计划
    dateFormat  YYYY-MM-DD
    section 阶段1
    任务1    :2024-01-01, 7d
    任务2    :2024-01-08, 5d
```

### 实际应用：软件开发进度

```mermaid
gantt
    title 软件开发进度
    dateFormat  YYYY-MM-DD
    section 规划
    需求分析    :2024-01-01, 10d
    系统设计    :2024-01-11, 15d
    section 开发
    编码        :2024-01-26, 30d
    测试        :2024-02-25, 15d
    section 发布
    部署上线    :2024-03-11, 5d
```

## 4. 类图 (Class Diagram)

### 基本语法

```mermaid
classDiagram
    class Animal{
        +String name
        +makeSound()
    }
    class Dog{
        +bark()
    }
    Animal <|-- Dog
```

### 实际应用：电商系统

```mermaid
classDiagram
    class Order{
        +String orderId
        +Date createTime
        +Double amount
        +process()
    }
    class OrderItem{
        +String productId
        +int quantity
        +Double price
    }
    class Product{
        +String productId
        +String name
        +Double price
    }
    Order "1" *-- "many" OrderItem
    OrderItem "1" --> "1" Product
```

## 5. 状态图 (State Diagram)

### 基本语法

```mermaid
stateDiagram-v2
    [*] --> 状态1
    状态1 --> 状态2
    状态2 --> [*]
```

### 实际应用：订单状态流转

```mermaid
stateDiagram-v2
    [*] --> 待支付
    待支付 --> 已支付: 用户付款
    已支付 --> 配送中: 商家发货
    配送中 --> 已完成: 用户收货
    待支付 --> 已取消: 超时/用户取消
    已完成 --> [*]
    已取消 --> [*]
```

## 6. 饼图 (Pie Chart)

### 基本语法

```mermaid
pie
    title 收入分布
    "A" : 30
    "B" : 20
    "C" : 50
```

### 实际应用：用户分布

```mermaid
pie
    title 用户地区分布
    "华东" : 35
    "华北" : 25
    "华南" : 20
    "西部" : 15
    "其他" : 5
```

## 使用提示

1. 在 Markdown 文件中使用时，将图表代码放在 \`\`\`mermaid 代码块中
2. 确保你的编辑器或平台支持 Mermaid 图表渲染
3. 可以使用在线 Mermaid 编辑器进行调试
4. 注意不同平台对 Mermaid 语法支持可能有差异
