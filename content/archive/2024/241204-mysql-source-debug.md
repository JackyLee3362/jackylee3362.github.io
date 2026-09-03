---
title: mysql-源码调试笔记
date: 2024-12-04
draft: true
author: JackyLee
tags:
categories:
cover:
  # image: 图片链接
  # alt: 文字内容
comment: true
---

## 问题记录

- [How to build and debug MySQL 8.x from source code](https://www.eversql.com/why-and-how-build-debug-mysql-from-source-code/)
- [mysql 启动报错 "unknown variable 'defaults-file=/etc/my.cnf" - 邱明成 - 博客园](https://www.cnblogs.com/qiumingcheng/p/11191759.html)

如何设置密码

Select User, authentication_string, host from mysql.user;

- [安装 mysql8.0.11 以及修改 root 密码、连接 navicat for mysql-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/1403537)
- [解决 Warning: World-writable config file ‘/etc/my.cnf’ is ignored-CSDN 博客](https://blog.csdn.net/a1010256340/article/details/77530131)
  配置文件权限问题，需要 755（不能是 777）

配置防火墙规则

- [WSL2 中安装 MySQL 并通过 Windows 连接 | M.P.O. Site](https://mysteriouspreserve.com/blog/2022/11/06/WSL2-MySQL/)

如何调试连接

handle_connection 函数断点

### static_cast 是什么

```cpp
int x = 5;
float y = static_cast<float>(x); // int 到 float 的转换
```

`static_cast` 是 C++ 中的一种类型转换操作符，用于在兼容类型之间进行显式的类型转换。与 C 风格的强制类型转换 (`(Type)variable`) 或其他 C++ 类型转换操作符（如 `dynamic_cast`, `const_cast` 和 `reinterpret_cast`）相比，`static_cast` 提供了更强的类型检查，能在编译时进行类型验证。

#### `static_cast` 的作用

`static_cast` 主要用于以下几种情况：

1. **在相关类型之间进行转换**： 例如，基类指针或引用可以转换为派生类指针或引用，前提是类之间有继承关系，并且转换是合法的。

cpp

复制代码

```cpp
class Base {
    public: virtual void show() {
        std::cout << "Base" << std::endl;
    }
};

class Derived : public Base {
    public: void show() override {
        std::cout << "Derived" << std::endl;
    }
};

Base* basePtr = new Derived();
Derived* derivedPtr = static_cast<Derived*>(basePtr);  // 合法转换
```

1. **基础数据类型之间的转换**： `static_cast` 可以用于将基本数据类型（如 `int` 转换为 `float`）之间的转换。

```cpp
int x = 5; float y = static_cast<float>(x);  // int 到 float 的转换
```

1. **转换为 `void*` 或从 `void*` 恢复**： `static_cast` 也可以用于将类型转换为 `void*`，或者将 `void*` 转回某个具体的类型。
2. **从派生类到基类的转换**： `static_cast` 可以用来进行显式的向上转换（从派生类到基类）。这通常是安全的，因为每个派生类对象都包含一个基类对象。

cpp

```cpp
class Base {}; class Derived : public Base {};  Derived d; Base* b = static_cast<Base*>(&d);  // 合法的向上转换
```

#### 在你的代码中的使用

```cpp
Channel_info *channel_info = static_cast<Channel_info *>(arg);
```

在这个例子中，`arg` 是一个 `void*` 或其他类型的指针，`static_cast<Channel_info *>` 将其转换为 `Channel_info*` 类型。这里的 `static_cast` 强制将 `arg` 指向的内存地址转换为 `Channel_info*` 类型，假设 `arg` 实际上是一个指向 `Channel_info` 类型的对象或指针。

#### `static_cast` 和其他类型转换操作符的区别

- **`static_cast`**：用于大多数类型之间的转换，要求类型之间有某种关系（如继承关系或基本数据类型之间的转换）。
- **`dynamic_cast`**：用于运行时类型安全检查，通常用于多态类型之间的转换（如从基类指针转换为派生类指针），如果转换不合法，`dynamic_cast` 返回 `nullptr`（对于指针）或抛出 `std::bad_cast` 异常（对于引用）。
- **`const_cast`**：用于添加或去除对象的 `const` 限定符。
- **`reinterpret_cast`**：用于进行低级的指针类型转换，可以将一个类型的指针直接转换为任何其他类型的指针，甚至是完全不相关的类型，通常很危险。

#### 总结

`static_cast` 是一种类型安全的转换方式，常用于类型之间的合法转换，且可以在编译时检查转换是否合法。它比 C 风格的强制转换更安全，避免了潜在的类型不匹配问题。

### `[[ maybe_used ]]` 是什么

这段代码中的 `[[maybe_unused]]` 是 C++17 引入的一种属性（attribute）语法，表示一个变量可能会被声明但不会使用。它用于告诉编译器，即使该变量没有被使用，也不要产生警告或错误。

如何调试 show databases;

如何调试 mysql select

## 参考资料

- [MySql 轻松入门系列——第二站 使用 visual studio 对 mysql 进行源码级调试 - 一线码农 - 博客园][]

[MySql轻松入门系列——第二站 使用visual studio 对mysql进行源码级调试 - 一线码农 - 博客园]: https://www.cnblogs.com/huangxincheng/p/13084736.html "MySql轻松入门系列——第二站 使用visual studio 对mysql进行源码级调试 - 一线码农 - 博客园"
