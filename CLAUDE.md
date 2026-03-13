# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个静态 HTML 网站，用于展示学校全景漫游（学校全景漫游），采用科幻风格主题。网站使用 Pannellum (v2.5.7) 来展示学校各地点的 360° 全景图像。

**无构建系统或框架** - 这是一个单 HTML 文件，包含内联的 CSS 和 JavaScript。

## 命令

- `npm run deploy` - 使用 gh-pages 包部署到 GitHub Pages

## 架构

### 单页应用结构

应用有两个通过 JavaScript 切换的主视图：

1. **地图视图** (`#map`)
   - 显示 `page.jpg` 作为学校地图
   - 包含定位的按钮（`.building-btn`）用于各个地点
   - 按钮位置通过内联 `style` 属性设置 `left` 和 `top` 百分比

2. **全景视图** (`#pano`)
   - 使用 Pannellum 查看器显示 360° 全景图像
   - 四个可用场景：computer（计算机）、gym（体育馆）、dance（舞蹈室）、eat（食堂）
   - 支持自动旋转、缩放和全屏控制

### 状态管理

- 全局 `viewer` 变量保存 Pannellum 实例
- `enterPano(sceneKey)` 函数从地图过渡到全景视图
- `backToMap()` 函数从全景视图返回地图

### 文件组织

- `index.html` - 完整的应用程序（HTML、CSS、JS）
- `page.jpg` - 学校地图背景图像
- `computer.jpg`、`gym.jpg`、`dance.jpg`、`eat.jpg` - 360° 全景图像
- `.gh-pagesignore` - 从 GitHub Pages 部署中排除的文件（排除 node_modules）

## 主题与样式

- **主题**：科幻/霓虹青色配色方案
- **颜色**：主色调青色 (#00f0ff)，深蓝色背景 (#0a0a1f, #000814)
- **字体**："Orbitron"（从外部源加载）
- **效果**：玻璃态、发光阴影、平滑过渡 (0.4-1.2s)

## 添加新全景

要添加新地点：

1. 将新的全景图像添加到根目录
2. 在 HTML 中添加按钮，设置适当的 `style="left: X%; top: Y%"` 定位
3. 在 `getPanoUrl()` 函数的 `urls` 对象中添加场景

示例：
```javascript
const urls = {
  // ...现有场景
  newlocation: "./newlocation.jpg",
};
```
