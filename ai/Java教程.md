# Java 编程教程

## 目录

1. [Java 简介](#java-简介)
2. [开发环境搭建](#开发环境搭建)
3. [Java 基础语法](#java-基础语法)
4. [数据类型和变量](#数据类型和变量)
5. [运算符](#运算符)
6. [控制流语句](#控制流语句)
7. [数组](#数组)
8. [面向对象编程](#面向对象编程)
9. [继承和多态](#继承和多态)
10. [接口和抽象类](#接口和抽象类)
11. [异常处理](#异常处理)
12. [Java 集合框架](#java-集合框架)
13. [泛型](#泛型)
14. [多线程编程](#多线程编程)
15. [Java I/O 操作](#java-io-操作)
16. [Java 网络编程](#java-网络编程)
17. [Java 8 新特性](#java-8-新特性)
18. [Java 项目实战](#java-项目实战)

## Java 简介

Java 是由 Sun Microsystems 公司于 1995 年推出的一种面向对象的编程语言，现在由 Oracle 公司所有。Java 具有以下特点：

- **跨平台性**：Java 程序可以在任何装有 Java 虚拟机（JVM）的设备上运行，不需要重新编译。
- **面向对象**：Java 是一种纯面向对象的语言，支持封装、继承、多态等面向对象特性。
- **简单性**：Java 语法简单，易于学习。
- **安全性**：Java 提供了多层次的安全机制。
- **健壮性**：Java 的强类型机制、异常处理和自动内存管理等特性使其更加健壮。
- **多线程**：Java 内置多线程支持。

### Java 的应用领域

- 企业级应用（如银行、电信等行业的后台系统）
- Web 应用开发
- 移动应用开发（Android）
- 大数据处理（Hadoop、Spark 等）
- 云计算
- 物联网应用

## 开发环境搭建

### JDK 安装

JDK（Java Development Kit）是 Java 开发的核心工具包，包含了 JRE（Java Runtime Environment）和开发工具。

1. 访问 [Oracle 官网](https://www.oracle.com/java/technologies/javase-downloads.html) 下载最新版本的 JDK。
2. 根据操作系统选择相应的安装包。
3. 安装 JDK 并设置环境变量：
   - JAVA_HOME：指向 JDK 安装目录
   - PATH：添加 %JAVA_HOME%/bin（Windows）或 $JAVA_HOME/bin（Unix/Linux）

### 验证安装

打开命令行终端，输入以下命令：

```bash
java -version
javac -version
```

如果显示版本信息，则说明安装成功。

### 集成开发环境（IDE）

推荐使用以下 IDE 进行 Java 开发：

- **IntelliJ IDEA**：功能强大，智能提示出色，有社区版（免费）和旗舰版（付费）。
- **Eclipse**：开源免费，插件丰富。
- **NetBeans**：开源免费，适合初学者。
- **Visual Studio Code**：轻量级编辑器，安装 Java 扩展后可用于 Java 开发。

## Java 基础语法

### 第一个 Java 程序

创建一个名为 `HelloWorld.java` 的文件：

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

编译和运行：

```bash
javac HelloWorld.java
java HelloWorld
```

### Java 程序结构

- **类（Class）**：Java 程序的基本单位，所有代码都必须在类中。
- **方法（Method）**：类中的函数，用于执行特定任务。
- **main 方法**：Java 程序的入口点，格式固定。
- **语句（Statement）**：执行特定操作的代码，以分号结束。
- **注释**：用于解释代码，不会被执行。

### 注释

Java 支持三种注释方式：

```java
// 单行注释

/*
 多行注释
 可以跨多行
*/

/**
 * 文档注释
 * 用于生成 JavaDoc 文档
 * @author 作者名
 */
```

## 数据类型和变量

### 基本数据类型

Java 有 8 种基本数据类型：

1. **整数类型**：
   - `byte`：8 位，范围 -128 到 127
   - `short`：16 位，范围 -32,768 到 32,767
   - `int`：32 位，范围 -2^31 到 2^31-1
   - `long`：64 位，范围 -2^63 到 2^63-1

2. **浮点类型**：
   - `float`：32 位，单精度浮点数
   - `double`：64 位，双精度浮点数

3. **字符类型**：
   - `char`：16 位，表示一个 Unicode 字符

4. **布尔类型**：
   - `boolean`：表示真（true）或假（false）

### 引用数据类型

- **类（Class）**
- **接口（Interface）**
- **数组（Array）**

### 变量声明和初始化

```java
// 声明变量
int age;
String name;

// 初始化变量
age = 25;
name = "John";

// 声明并初始化
int salary = 5000;
final double PI = 3.14159; // 常量，不可修改
```

### 类型转换

- **自动类型转换**（隐式转换）：小类型转换为大类型。

```java
byte b = 10;
int i = b; // 自动将 byte 转换为 int
```

- **强制类型转换**（显式转换）：大类型转换为小类型，可能会丢失精度。

```java
int i = 100;
byte b = (byte) i; // 强制将 int 转换为 byte
```

## 运算符

### 算术运算符

- `+`：加法
- `-`：减法
- `*`：乘法
- `/`：除法
- `%`：取余
- `++`：自增
- `--`：自减

### 关系运算符

- `==`：等于
- `!=`：不等于
- `>`：大于
- `<`：小于
- `>=`：大于等于
- `<=`：小于等于

### 逻辑运算符

- `&&`：逻辑与
- `||`：逻辑或
- `!`：逻辑非

### 位运算符

- `&`：按位与
- `|`：按位或
- `^`：按位异或
- `~`：按位取反
- `<<`：左移
- `>>`：右移
- `>>>`：无符号右移

### 赋值运算符

- `=`：简单赋值
- `+=`、`-=`、`*=`、`/=`、`%=`：复合赋值

### 三元运算符

```java
条件表达式 ? 表达式1 : 表达式2
```

## 控制流语句

### 条件语句

#### if 语句

```java
if (条件) {
    // 条件为真时执行的代码
}
```

#### if-else 语句

```java
if (条件) {
    // 条件为真时执行的代码
} else {
    // 条件为假时执行的代码
}
```

#### if-else if-else 语句

```java
if (条件1) {
    // 条件1为真时执行的代码
} else if (条件2) {
    // 条件2为真时执行的代码
} else {
    // 所有条件都为假时执行的代码
}
```

#### switch 语句

```java
switch (表达式) {
    case 值1:
        // 表达式等于值1时执行的代码
        break;
    case 值2:
        // 表达式等于值2时执行的代码
        break;
    default:
        // 表达式不等于任何 case 值时执行的代码
}
```

### 循环语句

#### for 循环

```java
for (初始化; 条件; 更新) {
    // 循环体
}
```

示例：

```java
for (int i = 0; i < 5; i++) {
    System.out.println("i = " + i);
}
```

#### while 循环

```java
while (条件) {
    // 循环体
}
```

示例：

```java
int i = 0;
while (i < 5) {
    System.out.println("i = " + i);
    i++;
}
```

#### do-while 循环

```java
do {
    // 循环体
} while (条件);
```

示例：

```java
int i = 0;
do {
    System.out.println("i = " + i);
    i++;
} while (i < 5);
```

### 跳转语句

- `break`：跳出循环或 switch 语句
- `continue`：跳过当前循环的剩余部分，继续下一次循环
- `return`：从方法返回

## 数组

### 数组声明和初始化

```java
// 声明数组
int[] numbers;
String[] names;

// 创建数组
numbers = new int[5]; // 创建一个长度为 5 的整数数组
names = new String[3]; // 创建一个长度为 3 的字符串数组

// 声明并创建数组
int[] scores = new int[10];

// 声明、创建并初始化数组
int[] values = {1, 2, 3, 4, 5};
String[] fruits = {"Apple", "Banana", "Orange"};
```

### 访问数组元素

```java
int[] numbers = {10, 20, 30, 40, 50};

// 访问数组元素
int firstNumber = numbers[0]; // 10
int thirdNumber = numbers[2]; // 30

// 修改数组元素
numbers[1] = 25;
```

### 数组长度

```java
int[] numbers = {10, 20, 30, 40, 50};
int length = numbers.length; // 5
```

### 遍历数组

```java
int[] numbers = {10, 20, 30, 40, 50};

// 使用 for 循环
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}

// 使用 for-each 循环（增强型 for 循环）
for (int number : numbers) {
    System.out.println(number);
}
```

### 多维数组

```java
// 声明并创建二维数组
int[][] matrix = new int[3][4]; // 3行4列的二维数组

// 声明、创建并初始化二维数组
int[][] grid = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// 访问二维数组元素
int value = grid[1][2]; // 6

// 遍历二维数组
for (int i = 0; i < grid.length; i++) {
    for (int j = 0; j < grid[i].length; j++) {
        System.out.print(grid[i][j] + " ");
    }
    System.out.println();
}
```

## 面向对象编程

### 类和对象

**类**是对象的模板或蓝图，**对象**是类的实例。