---
layout: ../../layouts/PostLayout.astro
title: Raylib库
date: "2026-05-20"
cover: "/images/study-cover.png"
categories: "C/C++"
mark: 2
---
> 本文是我从 C 转向 C++ 过程中的学习笔记。以教为学，若有疏漏，纯属正常。

> "学习知识不是学习的目的，解决自己的需求才是。"--Cymen

你是否想仅凭自己来制作游戏，同时觉得市面上的游戏引擎不是臃肿、繁杂，就是社区生态不成熟？那么，使用raylib库绝对是个不错的选择。

## 问题一：raylib是个什么样的库？
- 从语言上来说，它是用纯 C 代码（C99）编写的库，这也就代表着它同时也兼容 C++。

**C99是什么意思？**：指的是 C 语言在 1999 年发布的一个国际标准版本（正式名称为 ISO/IEC 9899:1999），引入了许多你现在觉得理所当然、但在当时是革命性的改进：单行注释、随处声明变量、for 循环内声明变量、布尔类型、指定初始化器 、变长数组（虽然这个特性在后来的 C11 中变成了可选）、long long 类型（正式支持 64 位整数）。

- 从技术上来说，它是个OpenGL的高级封装库，把复杂的、底层的 OpenGL 指令（比如处理缓冲区、顶点阵列等）封装成了非常简单的函数，得益于此，raylib也有了跨平台的功能。

**OpenGL 是什么？**：一套用来定义“图形软件如何与显卡硬件交互”的规范，还有类似的如：Vulkan、DirectX 12 更接近硬件，但也更难写，想了解更多就自己去搜索吧。

- 从功能上来说，它是个多媒体开发框架，它处理了开发一个游戏或交互式程序所需的全套功能：图形 (Graphics)、音频 (Audio)、输入 (Input)、数学 (Math)，甚至是 VR 支持。

**raylib有哪些功能？**：可以通过[官方中文文档](https://www.raylib.com/cheatsheet/cheatsheet_zh.html)来做参考与辅助学习。

## 问题二：raylib的设计理念是什么？
它的创始人 Ramon Santamaria 给 raylib 注入了非常独特的技术性格。这个设计理念可以被总结为一句话：“享受编程，简单至上” (A simple and easy-to-use library to enjoy videogames programming)。
1. **极简主义与教育导向**：raylib 最初是为教育设计的，旨在让学生摆脱复杂的底层配置，直接进入编程的核心。
2. **无外部依赖**：所有必需的库都已包含在 raylib 中。
3. **用纯 C 代码 (C99) 编写**：采用 PascalCase/camelCase 命名法。
4. **即时模式风格的 API (Immediate-mode-like API)**：它强调“**每一帧都重画一切**”，这种“数据驱动渲染”的思路非常直观，也非常有趣，可以引发学生对渲染技术由浅入深的思考。
5. **免费开源软件**：raylib 采用未经修改的 zlib/libpng 许可证，该许可证是符合 OSI 标准的类 BSD 许可证，允许静态链接闭源软件。

## 问题三：raylib有缺点吗？
有，为了保持简单，它放弃了复杂的功能；为了保持透明，它放弃了自动化的管理。
- **缺乏面向对象特性**：虽然 raylib 与 C++ 兼容，但它的底层是 C，没有命名空间、没有类、没有继承、没有多态，不过你可以通过再封装一层来手动解决这个问题。
- **内存管理压力**：它没有 RAII（资源获取即初始化）。如果你 LoadTexture 了但忘了 UnloadTexture，就会内存泄漏。它不会像现代 C++ 对象那样在析构时自动清理。
- **raylib 支持 3D，但不完全支持**：它缺乏延迟渲染（Deferred Rendering）、高级全动态光照、物理渲染（PBR）的深度支持。
- **线程安全问题**：raylib 的大部分绘图函数不是线程安全的。这意味着你很难在后台线程里进行复杂的渲染操作，所有的绘图指令必须在主线程后执行。

## 问题四：raylib使用者为什么这么少呢？
- 希腊奶。

**希腊奶是什么意思？**：不知道。

## 问题五：raylib为什么被我所喜爱？
Raylib 没有铺天盖地的类（Class），没有复杂的命名空间，没有强迫你使用的设计模式。它用最纯正的 C 语言写成，它的核心循环代码干净得让人感动：

```c
#include "raylib.h"

int main(void) {
    // 1. 初始化
    InitWindow(800, 600, "Raylib");

    // 2. 核心循环
    while (!WindowShouldClose()) {
        BeginDrawing();
            ClearBackground(RAYWHITE);
            DrawText(“I think, therefore I am.”, 190, 300, 20, DARKGRAY);
        EndDrawing();
    }

    // 3. 释放资源
    CloseWindow();
    return 0;
}
```
Raylib 完美契合了我目前的学习状态。它既能让我用 C++ 进行更高维度的逻辑抽象，又保留了 C 语言级别的底层透明度。

如果我想，我随时可以制作一款小游戏以作为消遣。
## 结语：
在技术日新月异的今天，总有人在拼命做加法。但 Raylib 证明了，做减法，回归编程最初的纯粹，依然能让人热血沸腾。