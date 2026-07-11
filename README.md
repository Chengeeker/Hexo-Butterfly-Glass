# Hexo-Butterfly-Liquid-Glass

<p align="center">
<a href="./README.md">中文</a> | <a href="./README_EN.md">English</a>
</p>

<p align="center">
<strong>一个为 Hexo Butterfly 主题打造的模块化 Liquid Glass UI 增强系统。</strong><br>
在不修改主题源码的前提下，为 Butterfly 引入 Apple 风格 Liquid Glass 与 Material You 深色设计语言。
</p>

---

## ✨ 项目简介

**Hexo-Butterfly-Liquid-Glass** 是一个针对 Hexo Butterfly 主题开发的视觉增强项目。本项目通过独立的 CSS 模块，对 Butterfly 主题进行非侵入式 UI 增强，将现代操作系统（如 Apple Liquid Glass、macOS 半透明界面、iOS 控制中心、visionOS 空间化 UI 以及 Android Material You）的设计语言引入博客界面。

项目的核心理念是 **“Enhance, don't replace”（增强，而非替代）**。

我们不会修改 Butterfly 主题的底层源码，而是通过 CSS Override Layer（CSS 覆盖层）来实现视觉升级。这种非侵入式设计带来了以下优势：
- **兼容性强**：Butterfly 主题更新不会覆盖自定义修改。
- **维护成本低**：模块化 CSS 易于排查和修改。
- **迁移便捷**：支持在不同 Hexo 站点间快速复用。
- **灵活控制**：支持随时启用或关闭增强效果。

---

## 🌟 核心特性

### 🪟 Liquid Glass 玻璃化系统
将 Butterfly 原有组件升级为现代玻璃拟态 UI。通过 `backdrop-filter`、半透明 Surface、多层阴影、边框透明度及高光反射等技术，实现类似 macOS Toolbar、iOS Panel 和 visionOS Window 的视觉质感。
- **覆盖组件**：首页文章卡片、侧边栏组件、右侧功能按钮、文章目录（TOC）、顶部导航栏。

### 🌈 环境光背景系统
通过纯 CSS 构建动态环境背景，摒弃传统的固定背景图片方案。采用多层渐变与环境光效果，结合玻璃折射与空间层次，营造类似 macOS Sonoma 壁纸与 visionOS 空间视觉的沉浸感。支持 Light/Dark 模式独立设计，且无额外图片依赖。

### 🌙 Material You 深色模式
摒弃传统纯黑（`#000000`）深色模式带来的强烈对比与阅读疲劳，同时避免纯黑背景导致玻璃效果失效的问题。采用“深灰 Surface + 环境色 + 低亮度玻璃层”的组合，在提升阅读舒适度的同时，保持现代系统的质感与视觉连贯性。

### 🍎 悬浮式玻璃导航 (Floating Glass Navbar)
重新设计顶部导航栏，采用悬浮式布局与圆角玻璃设计。结合毛玻璃背景与阴影层次，完美适配深浅模式，设计灵感源自 macOS Toolbar 与 visionOS Floating Panel。

### 🏷️ 胶囊标签系统 (Capsule Tag System)
将默认的扁平标签优化为现代胶囊风格（Capsule UI），参考 iOS Tag、Material Chip 与 macOS Label 的设计规范，提升界面的精致度与现代感。

---

## 🏗️ 设计架构

本项目严格遵循**非侵入式设计**原则。架构层级如下：

```text
Butterfly Theme (原生主题)
       ↓
CSS Override Layer (本项目 CSS 覆盖层)
       ↓
Liquid Glass System (最终视觉呈现)
```

**不修改的内容**：Butterfly 源文件、JavaScript 逻辑、模板结构。  
**确保的结果**：主题升级无缝衔接，扩展模块独立运行。

---

## 📂 项目结构与模块说明

```text
butterfly-liquid-glass/
└── css/
    ├── liquid-variable.css   # 全局设计变量（圆角、阴影、模糊、颜色等）
    ├── liquid-background.css # 页面背景系统（Light/Dark 模式背景）
    ├── liquid-ambient.css    # 环境光系统（柔和反射、色彩氛围、空间层次）
    ├── liquid-glass.css      # 核心玻璃组件（卡片、侧边栏、功能按钮）
    ├── liquid-navbar.css     # 顶部悬浮玻璃导航
    ├── liquid-post.css       # 文章页面增强（内容 Surface、阅读体验优化）
    ├── liquid-tag.css        # 标签胶囊系统
    ├── liquid-toc.css        # 文章目录玻璃化
    └── liquid-config.css     # 最终覆盖层（权重修正、兼容补丁、特殊调整）
```

**核心模块解析**：
- **`liquid-variable.css`**：全局设计变量系统，集中管理 `--lg-radius-xl`、`--lg-blur-heavy` 等核心参数。
- **`liquid-glass.css`**：核心视觉实现，大量运用 `backdrop-filter`、`rgba()`、`box-shadow` 构建玻璃质感。
- **`liquid-config.css`**：作为最终的覆盖层，负责 CSS 权重修正与 Butterfly 的兼容补丁。

---

## 🚀 安装指南

### 1. 克隆项目
```bash
git clone https://github.com/yourname/Hexo-Butterfly-Liquid-Glass.git
```

### 2. 部署文件
将 `butterfly-liquid-glass` 文件夹复制到 Hexo 站点的 `source/` 目录下。  
最终路径应为：`source/butterfly-liquid-glass/css/`。

### 3. 引入 CSS
修改 Hexo 根目录下的 `_config.yml`，在 `inject` -> `head` 中按顺序引入以下 CSS 文件（**注意顺序，变量文件需最先引入**）：

```yaml
inject:
  head:
    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-variable.css">
    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-background.css">
    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-ambient.css">
    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-glass.css">
    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-navbar.css">
    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-post.css">
    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-tag.css">
    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-toc.css">
    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-config.css">
```

### 4. 生成与预览
```bash
hexo clean
hexo generate
hexo server
```

---

## 📱 浏览器兼容性

本项目依赖现代 CSS 特性，推荐使用以下浏览器的最新版本：
- Chrome / Edge
- Safari
- Firefox

**核心依赖**：浏览器需完整支持 CSS `backdrop-filter` 属性。

---

## ❌ 已移除方案 (Design Trade-offs)

在开发过程中，我们测试了部分视觉方案，但为了保障博客的核心阅读体验，最终进行了克制与移除：

| 移除方案 | 移除原因 |
| :--- | :--- |
| **顶部图全局融合** | 深色模式下表现不稳定，且容易干扰正文阅读。 |
| **右侧浮岛控制中心** | 占用正文内容空间，在移动端设备上体验下降明显。 |
| **额外 Hover 动画** | Butterfly 原生交互已足够完善，额外动画视觉收益有限且易显繁杂。 |
| **封面图片融合动画** | 破坏了博客固有的阅读节奏与沉浸感。 |

**最终原则**：保持 Butterfly 的博客属性，只做视觉增强，不干扰内容消费。

---

## 🛣️ Roadmap

- [ ] 适配更多 Butterfly 原生页面
- [ ] 扩展 Material You 动态配色方案
- [ ] 开发自动化配置与主题生成工具
- [ ] 移植至 Astro / Hugo 等其他静态站点生成器
- [ ] 支持更多自定义 UI 组件

---

## 🤝 参与贡献

欢迎通过 Issue 或 Pull Request 参与贡献，包括但不限于：
- 新增 UI 组件或视觉效果
- 修复已知 Bug 或样式冲突
- 优化浏览器兼容性
- 完善文档与翻译

---

## 📄 License

本项目基于 [MIT License](./LICENSE) 开源。

---

## ❤️ 致谢

- [Hexo Butterfly Theme](https://github.com/jerryc127/hexo-theme-butterfly)：提供优秀的主题基础。
- **Apple Design Language**：提供 Liquid Glass 与空间化 UI 的设计灵感。
- **Material Design Community**：提供 Material You 深色模式与动态色彩的参考。

---

<p align="center">
<strong>Made with ❤️ for Hexo Butterfly users.</strong>
</p>
