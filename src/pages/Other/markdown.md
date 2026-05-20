---
layout: ../../layouts/PostLayout.astro
title: markdown语法测试
date: "2026-05-08"
cover: "/images/post-cover.jpg"
categories: "Other"
mark: 2
---
## 1.标题
使用 # 号， # 越多标题越小（支持1~6级）。
\# 一级标题
\## 二级标题

## 2.强调
***斜体***：\*这是斜体\*或\_这是斜体\_
*这是斜体*
**加粗**：\*\*这是粗体\*\*或\_\_这是粗体\_\_
**这是粗体**

## 3.引用
>引用内容
**基础引用**：
>>嵌套的内容
**嵌套引用**：

**包含其他元素**：引用中可以包含标题、列表或加粗。

## 4.列表(List)
**无序列表**：使用*、+、-。
- C++20
- Raylib
- Qt 6

**有序列表**：数字加点（如1.）。
1. 需求分析
2. 架构设计
3. 编码实现

**嵌套列表**：在子列表前缩进2或4个空格。

## 5.代码(Code)
**代码块**：\`\`\`(指定语言)
\`\`\`
```C++
cout << "Hello World" << endl;
```

## 6.表格(Tables)
|项目（左对齐）|价格（居中）|备注（右对齐）|
|:---|:--:|---:|
|电脑|5000|不要辣|
|手机|3000|微辣|
|耳机|200|辣|

## 7.删除线： \~\~已作废内容\~\~
~~已作废内容~~

## 8.链接与图片
返回 [首页](/my-blog-Astro/)

![图片加载失败](/public/images/avatar.png "头像")
<!-- **行内链接**：[Home](/ "Homo")
**行内链接**：[My-New-Post](/2026/05/05/My-New-Post/ "My-New-Post")
**引用式链接**：
正文：[GitHub](https://github.com)
文末定义：[repo]: https://github.com "前往 GitHub"
**自动链接**：<https://github.com/>
**图片**：![替代文字](public/images/avatar.jpg "提示文字") -->

## 9.转义文字：在符号前加\。
**支持转义**：\, `, *, _, {, }, [, ], (, ), #, +, -, ., !, |。

## 10.数学公式(LaTeX)：【目前没装插件】
**行内**：$ E = mc^2 $
**块状**：$$ \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} $$

## 11.原生HTML
Markdown兼容大部分HTML标签。
<input type="checkbox"> 我是手动点击的
<input type="checkbox" checked> 我也可以取消勾选
<u>下划线</u>
<details>
<summary>点击查看代码测试结果</summary>
这里是隐藏的内容，啪嗒啪嗒...
</details>

## 12.Emoji
WIN+逗号：smile😂。