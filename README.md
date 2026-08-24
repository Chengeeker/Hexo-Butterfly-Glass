# Hexo Butterfly Glass

[English](README_EN.md)

一个面向 Hexo Butterfly 主题的模块化 Liquid Glass / Glassmorphism 视觉增强系统。

本项目不修改 Butterfly 主题源码，而是通过独立 CSS、Runtime JavaScript 和 Hexo 注入配置，为 Butterfly 增加：

- Light / Dark 双主题玻璃材质
- CSS Glass Environment 环境光背景
- 背景透射、模糊与饱和度
- 边缘高光、内阴影与景深
- 文章页 Surface Hierarchy
- Archive、首页卡片、侧栏、说说页面适配
- 移动端性能降级
- 右侧悬浮控制与作者卡片玻璃按钮
- 轻量标签与分享按钮样式

## 当前版本特性

### Glass Environment

环境背景不是简单的纯白或纯黑，而是由 CSS 构建的低饱和环境光场：

- Light：近白色基础、蓝色/紫色/暖色柔和光晕
- Dark：深灰基础、蓝紫色环境光和少量青色区域
- 使用 `body` 作为实际背景容器，并保留 `#web_bg` 兼容选择器
- 移动端自动降低背景固定和模糊成本

### Surface Hierarchy

页面遵循以下层级：

```text
Environment
    ↓
Primary Glass Surface
    ↓
Transparent Content Layer
```

文章页中：

- `#post` 是主要 Glass Surface
- `#article-container` 是透明内容层
- 正文、代码块、文章标签和分享按钮不会重复创建新的 `backdrop-filter`
- 说说页面由于没有 `#post`，每个 `.shuoshuo-item` 使用独立 Glass Surface

### Light / Dark Controls

- 首页作者信息卡和 Follow Me 按钮支持双主题
- Light 模式使用浅色半透明按钮和深色图标
- Dark 模式使用深色半透明按钮和浅色图标
- 微信、QQ 等分享按钮采用低亮度边缘高亮
- 文章标签不再使用大面积高光和强阴影

### Runtime Performance

`js/glass-runtime.js` 负责：

- 浏览器 `backdrop-filter` 能力检测
- Full / Reduced / Fallback / Disabled 状态
- 移动端默认降级
- Reduced Motion 支持
- Desktop Fine Pointer 光照交互

## 项目结构

```text
butterfly-glass/
├── css/
│   ├── glass-tokens.css        # 设计变量、主题、圆角、阴影、性能参数
│   ├── glass-environment.css   # 页面环境光与背景层
│   ├── glass-core.css          # 核心 Glass Surface
│   ├── glass-optical.css       # 光学高光与交互光照
│   ├── glass-depth.css         # 景深与层次
│   ├── glass-archive.css       # Archive 页面
│   ├── glass-post.css          # 文章页层级与阅读内容
│   ├── glass-page.css          # 说说、作者卡片和页面控件
│   ├── glass-responsive.css    # Mobile / Tablet / Desktop
│   ├── glass-navbar.css        # 顶部导航
│   ├── glass-tag.css           # 标签和分享控件
│   ├── glass-toc.css           # TOC
│   └── glass-search.css        # 搜索弹窗
├── js/
│   └── glass-runtime.js        # 能力检测与性能状态
├── config_butterfly_glass.yml  # 可选配置示例
└── glass-state.json            # 状态记录
```

## 安装

将 `butterfly-glass/` 复制到 Hexo 项目的 `source/` 目录：

```text
Your-Hexo-Site/
├── _config.butterfly.yml
└── source/
    └── butterfly-glass/
```

在 Butterfly 的 `_config.butterfly.yml` 中按以下顺序注入：

```yaml
inject:
  head:
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-tokens.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-environment.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-core.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-optical.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-depth.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-archive.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-post.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-page.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-responsive.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-navbar.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-tag.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-toc.css">
    - <link rel="stylesheet" href="/butterfly-glass/css/glass-search.css">

  bottom:
    - <script src="/butterfly-glass/js/glass-runtime.js"></script>
```

`glass-tokens.css` 必须最先加载。不要删除它，否则所有 `--lg-*` 变量都会失效。

## 配置 Runtime

可以在 Runtime 加载前设置：

```html
<script>
  window.ButterflyGlassConfig = {
    enabled: true,
    mobileFullGlass: false,
    pointerOptical: true,
    reducedMode: 'auto'
  }
</script>
```

支持的 `reducedMode`：

- `auto`：根据浏览器、设备和无障碍偏好自动选择
- `full`：使用完整 Glass，浏览器不支持时自动回退
- `reduced`：使用降低后的 Glass
- `fallback`：关闭模糊和高成本光学效果

## 开发与验证

```bash
npm install
npx hexo generate
npx hexo server
```

当前验证环境：

- Hexo 8.1.2
- Butterfly 5.7.0
- Chrome / Edge / Firefox / Safari 现代版本目标
- Desktop 与 Mobile
- Light / Dark

已经验证的页面类型：

- 首页
- Archive
- 文章页
- 说说
- 自定义页面

重点验证项目：

- `#post` 与 `#article-container` 不产生嵌套 Glass
- 说说动态生成的 `.shuoshuo-item` 使用 Glass
- Light / Dark 下 Follow Me 图标和文字清晰
- 微信、QQ 分享按钮不产生过强高光
- Mobile 默认使用 Reduced Glass

## 本版更新摘要

- 重构 Glass Environment，使环境光真正绑定到 Butterfly 5.7.0 的 `body` 背景容器
- 建立 `#post` / `#article-container` 的 Surface Hierarchy
- 修复 `glass-navbar.css` 和 Runtime 的资源路径
- 增加 `glass-page.css`，适配说说页面与作者卡片控件
- 修复 Follow Me 的 Light / Dark 玻璃按钮样式
- 拆分文章标签和 Share.js 分享图标样式
- 降低深色模式下标签、微信、QQ 分享按钮的高光和阴影
- 建立统一 Radius System
- 增加移动端 Blur、Radius 和性能降级规则
- 修复搜索模块中不存在的旧变量引用
- 通过 Hexo 构建验证

## 最终修改文件清单

同步本版时，优先复制以下文件：

```text
css/glass-tokens.css
css/glass-environment.css
css/glass-core.css
css/glass-post.css
css/glass-page.css
css/glass-tag.css
css/glass-archive.css
css/glass-responsive.css
css/glass-search.css
css/glass-toc.css
js/glass-runtime.js
config_butterfly_glass.yml
glass-state.json
README.md
README_EN.md
```

如果使用本项目随附的博客配置，还需要同步 Butterfly 配置中的注入入口，尤其确认路径始终是：

```text
/butterfly-glass/
```

不要改成 `butterfly-glass-v4/`、`butterfly-glass-v5/` 或其他版本化目录。

## 设计原则

- Enhance, don't replace
- 一个视觉区域原则上只使用一个主要 Glass Surface
- Glass 内部默认不再使用 `backdrop-filter`
- 优先使用 Environment 提供材质变化
- 不通过无限增加透明度或 Blur 强度制造玻璃感
- 不修改 Butterfly 主题源码
- 视觉效果必须为内容阅读服务

## License

MIT License

## Credits

- [Hexo](https://hexo.io/)
- [Butterfly Theme](https://github.com/jerryc127/hexo-theme-butterfly)
- Apple Liquid Glass / visionOS design language
- Material Design / Material You
