---
layout: ../../layouts/PostLayout.astro
title: "使用git把blog上传到github"
date: "2026-05-16"
cover: "/images/post-cover.png"
categories: "About Blog & Me" 
mark: 3
---
## 1.修改 Astro 配置文件
打开你项目根目录下的 astro.config.mjs 文件，我们需要在里面配置一下你的网站地址。

如果你打算在 GitHub 上创建一个名为 my-blog 的仓库，请修改为以下内容：
```JavaScript
import { defineConfig } from 'astro/config';

export default defineConfig({
  // 把你的 GitHub 用户名替换到下面
  site: 'https://<你的用户名>.github.io', 
  // 你的 GitHub 仓库名字（必须加斜杠）
  base: '/my-blog', 
});
```
注意：如果你以后想买一个自己的域名，只要把这里的 site 改掉就可以了。

## 2.把代码推送到 GitHub
1.在 GitHub 上新建一个仓库：

2.登录 GitHub。

3.点击右上角的 "+" -> New repository。

4.Repository name 填入 my-blog（和上面 base 里写的一致）。

5.勾选 Public（公开）。

6.千万不要勾选 "Add a README file"（保持仓库为空）。

7.点击 Create repository。

8.在本地终端执行 Git 命令：
回到你的 VS Code 终端（确保你在博客项目目录下），如果你没关掉 npm run dev，可以按 Ctrl + C 退出运行状态，然后按顺序输入以下命令（复制粘贴即可）：
code
```Bash
# 初始化 git
git init

# 把所有文件添加到暂存区
git add .

# 提交代码并写上备注
git commit -m "初始化我的梦幻博客"

# 将主分支命名为 main
git branch -M main

# 关联到你刚刚创建的 GitHub 仓库 (把下面这行换成你 GitHub 页面上显示的仓库链接)
git remote add origin https://github.com/<你的用户名>/my-blog.git

# 推送代码到 GitHub
git push -u origin main
```

## 3.设置自动化部署 (GitHub Actions)
以前部署博客很麻烦，每次写完文章都要手动打包。现在我们可以用 GitHub 的“机器人”帮你全自动打包发布。

在你的项目里，依次新建文件夹：.github/workflows/（注意前面有个点）。

在里面新建一个文件叫 deploy.yml。

(完整路径：你的项目/.github/workflows/deploy.yml)

把下面这段官方标准的部署代码直接粘贴进去，一个字都不用改：
```Yaml
# 1. 工作流名称：显示在 GitHub Actions 页面上的标题
name: Deploy to GitHub Pages

# 2. 触发条件：什么时候启动这个机器人
on:
  push:
    branches: [ main ]  # 当你执行 git push 并且分支是 main 时触发
  workflow_dispatch:      # 允许你在 GitHub 网页上点按钮手动触发（方便调试）

# 3. 权限设置：机器人需要什么权限来操作你的仓库
permissions:
  contents: read        # 机器人需要读取你的代码文件
  pages: write          # 机器人需要有权把打包好的网页写入 Pages 服务
  id-token: write       # 安全验证所需的令牌权限

# 4. 任务流程：分为【打包 (build)】和【部署 (deploy)】两个阶段
jobs:
  # 阶段一：打包
  build:
    runs-on: ubuntu-latest  # 在 GitHub 提供的最新版 Linux 虚拟机上运行
    steps:
      - name: Checkout your repository using git
        uses: actions/checkout@v4  # 第一步：把你的代码下载到虚拟机里

      - name: Setup Node.js
        uses: actions/setup-node@v4 # 第二步：安装运行环境
        with:
          node-version: 22          # 【注意点】必须指定为 22，因为 Astro 6 不支持旧版 Node
          cache: 'npm'              # 开启缓存，下次部署时安装插件会飞快

      - name: Install, build, and upload your site
        uses: withastro/action@v2  # 第三步：由 Astro 官方机器人执行 npm install 和 npm run build

  # 阶段二：部署
  deploy:
    needs: build                   # 【注意点】必须等 build 任务成功后，才开始部署
    runs-on: ubuntu-latest
    environment:
      name: github-pages           # 部署到 GitHub Pages 环境
      url: ${{ steps.deployment.outputs.page_url }} # 部署成功后，返回你的博客网址
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4 # 第四步：把打包好的静态 HTML 发布到网上
```
保存后，把这个新文件也推送到 GitHub：
```Bash
git add .
git commit -m "添加自动部署配置"
git push
```

## 4.在 GitHub 上开启网页服务
回到你的 GitHub my-blog 仓库网页。

点击上方的 Settings (设置) 选项卡。

在左侧菜单往下找，点击 Pages。

在 Build and deployment 区域：

找到 Source，将下拉菜单从 Deploy from a branch 改为 GitHub Actions。