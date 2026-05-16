---
layout: ../layouts/PostLayout.astro
title: "早期像素艺术"
date: "2024-04-08"
description: "探讨复古像素艺术中的抖动算法..."
cover: "/images/post1-cover.jpg"
categories: "计算机图形学" 
mark: 2
---

我非常喜欢复古的像素艺术。前段时间了解了有关早期 Windows 系统的屏幕保护程序的故事，其中提到的一款发布于 1990 年代的屏保 `After Dark: Starry Night`，在黑色的屏幕上随机绘制闪光的像素形成星空和星空下的城市，我很喜欢。

## 什么是抖动 (Dithering)？

在计算机图形学中，**抖动**是一种有意造成的噪音，用于随机化量化误差。简单来说，就是当你的显示器只能显示有限的颜色（比如只有黑和白）时，如何骗过人眼，让人觉得画面有灰度。

> "The brain is wider than the sky." 
> 我们的大脑会自动把密集的黑白像素混合成灰色。

### 常见的抖动算法
目前常见的算法主要有以下几种：
1. **随机抖动 (Random Dithering)**：最简单，但噪点明显。
2. **Floyd-Steinberg 误差扩散**：效果最好，但计算复杂。
3. **有序抖动 (Ordered Dithering)**：我们今天要讨论的主角。

## Bayer 有序抖动

Bayer 抖动使用一个特殊的矩阵（Bayer Matrix）来决定某个像素应该是黑色还是白色。这种算法具有极强的规律性和几何美感。

### 算法实现代码演示

下面是一段简化的 C++ 伪代码，展示了如何使用 4x4 的 Bayer 矩阵对图像进行处理：

```cpp
// 4x4 Bayer Matrix
const int bayerMatrix[4][4] = {
    { 0,  8,  2, 10},
    {12,  4, 14,  6},
    { 3, 11,  1,  9},
    {15,  7, 13,  5}
};

void applyOrderedDither(Image& img) {
    for (int y = 0; y < img.height; y++) {
        for (int x = 0; x < img.width; x++) {
            // 获取当前像素的灰度值 (0-255)
            int pixelVal = img.getPixel(x, y);
            
            // 归一化后与矩阵对比
            int threshold = bayerMatrix[y % 4][x % 4] * 16;
            
            if (pixelVal > threshold) {
                img.setPixel(x, y, COLOR_WHITE);
            } else {
                img.setPixel(x, y, COLOR_BLACK);
            }
        }
    }
}