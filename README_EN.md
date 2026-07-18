# Hexo-Butterfly-Liquid-Glass

<p align="center">
<a href="./README.md">中文</a> | <a href="./README_EN.md">English</a>
</p>

<p align="center">
<strong>A modular Liquid Glass UI enhancement system built for the Hexo Butterfly theme.</strong><br>
Introducing Apple-style Liquid Glass and Material You dark design language to Butterfly without modifying the original theme source code.
</p>

---

## ✨ Introduction

**Hexo-Butterfly-Liquid-Glass** is a visual enhancement project developed specifically for the Hexo Butterfly theme. Through independent CSS modules, it provides a non-intrusive UI upgrade, bringing modern operating system design languages (such as Apple Liquid Glass, macOS translucent interfaces, iOS Control Center, visionOS spatial UI, and Android Material You) into the blog interface.

The core philosophy of this project is **"Enhance, don't replace."**

We do not modify the underlying source code of the Butterfly theme. Instead, visual upgrades are achieved through a CSS Override Layer. This non-intrusive design offers the following advantages:
- **High Compatibility**: Theme updates will not overwrite your custom modifications.
- **Low Maintenance Cost**: Modular CSS makes troubleshooting and editing straightforward.
- **Easy Migration**: Supports quick reuse across different Hexo sites.
- **Flexible Control**: The enhancement effects can be enabled or disabled at any time.

---

## 🌟 Core Features

### 🪟 Glass morphism UI system
Upgrades original Butterfly components into modern glass UI. By utilizing `backdrop-filter`, semi-transparent surfaces, multi-layer shadows, border transparency, and specular highlights, it achieves a visual texture similar to macOS Toolbars, iOS Panels, and visionOS Windows.
- **Covered Components**: Homepage post cards, sidebar widgets, right-side action buttons, Table of Contents (TOC), and the top navigation bar.

### 🌈 Ambient Background System
Constructs a dynamic ambient background using pure CSS, abandoning the traditional fixed background image approach. It employs multi-layer gradients and ambient light effects, combined with glass refraction and spatial hierarchy, to create an immersive experience akin to macOS Sonoma wallpapers and visionOS spatial visuals. It supports independent designs for Light/Dark modes with zero additional image dependencies.

### 🌙 Material You Dark Mode
Rejects the strong contrast and reading fatigue caused by traditional pure black (`#000000`) dark modes, while also avoiding the issue where pure black backgrounds nullify glass effects. It adopts a combination of "dark gray Surface + ambient colors + low-brightness glass layers," improving reading comfort while maintaining the texture and visual coherence of modern systems.

### 🍎 Floating Glass Navbar
Redesigns the top navigation bar with a floating layout and rounded glass design. Combined with a frosted glass background and shadow hierarchy, it perfectly adapts to both light and dark modes, drawing design inspiration from macOS Toolbars and visionOS Floating Panels.

### 🏷️ Capsule Tag System
Optimizes default flat tags into a modern capsule style (Capsule UI). Referencing the design specifications of iOS Tags, Material Chips, and macOS Labels, it enhances the refinement and modern feel of the interface.

---

## 🏗️ Design Architecture

This project strictly adheres to the principle of **non-intrusive design**. The architectural hierarchy is as follows:

```text
Butterfly Theme (Original Theme)
       ↓
CSS Override Layer (Project CSS Override Layer)
       ↓
Liquid Glass System (Final Visual Presentation)
```

**What remains unmodified**: Butterfly source files, JavaScript logic, and template structures.  
**What is ensured**: Seamless theme upgrades and independent operation of the extension modules.

---

## 📂 Project Structure & Module Description

```text
butterfly-liquid-glass/
└── css/
    ├── liquid-variable.css   # Global design variables (border-radius, shadows, blur, colors, etc.)
    ├── liquid-background.css # Page background system (Light/Dark mode backgrounds)
    ├── liquid-ambient.css    # Ambient light system (soft reflections, color atmosphere, spatial hierarchy)
    ├── liquid-glass.css      # Core glass components (cards, sidebars, action buttons)
    ├── liquid-navbar.css     # Top floating glass navigation
    ├── liquid-post.css       # Post page enhancement (content Surface, reading experience optimization)
    ├── liquid-tag.css        # Capsule tag system
    ├── liquid-toc.css        # Glassmorphism for Table of Contents
    └── liquid-config.css     # Final override layer (specificity correction, compatibility patches, special tweaks)
```

**Core Module Breakdown**:
- **`liquid-variable.css`**: The global design variable system, centrally managing core parameters like `--lg-radius-xl` and `--lg-blur-heavy`.
- **`liquid-glass.css`**: The core visual implementation, heavily utilizing `backdrop-filter`, `rgba()`, and `box-shadow` to build the glass texture.
- **`liquid-config.css`**: Acts as the final override layer, responsible for CSS specificity corrections and Butterfly compatibility patches.

---

## 🚀 Installation Guide

### 1. Clone the Project
```bash
git clone https://github.com/yourname/Hexo-Butterfly-Liquid-Glass.git
```

### 2. Deploy Files
Copy the project folder into the `source/` directory of your Hexo root.  
The final path should be: `Your Blog/source/butterfly-liquid-glass`.

### 3. Inject CSS
Modify the `_config.butterfly.yml` file in the root directory of your Hexo site. Under `inject` -> `head`, include the following CSS files in order (**Note the order: the variable file must be imported first**):

```yaml
inject:
  head:
    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-variable.css">

    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-background.css">

    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-page.css">

    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-glass.css">

    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-ambient.css">

    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-navbar.css">

    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-post.css">

    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-tag.css">

    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-toc.css">

    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-search.css">

    - <link rel="stylesheet" href="/butterfly-liquid-glass/css/liquid-config.css">
```

### 4. Generate and Preview
```bash
hexo clean
hexo generate
hexo server
```

---

## 📱 Browser Compatibility

This project relies on modern CSS features. The latest versions of the following browsers are recommended:
- Chrome / Edge
- Safari
- Firefox

**Core Dependency**: The browser must fully support the CSS `backdrop-filter` property.

---

## ❌ Design Trade-offs (Removed Features)

During development, we tested several visual approaches but deliberately removed them to preserve the core reading experience of the blog:

| Removed Feature | Reason for Removal |
| :--- | :--- |
| **Top Banner Global Blending** | Unstable performance in dark mode; easily distracts from reading the main content. |
| **Floating Control Center** | Occupies main content space; significantly degrades the experience on mobile devices. |
| **Extra Hover Animations** | Butterfly's native interactions are already sufficient; extra animations offer limited visual ROI and can look cluttered. |
| **Cover Image Blending Animations** | Disrupts the inherent reading rhythm and immersion of a blog. |

**Final Principle**: Maintain the blog-centric nature of Butterfly. Enhance the visuals only, without interfering with content consumption.

---

## 🛣️ Roadmap

- [ ] Adapt to more native Butterfly pages
- [ ] Expand Material You dynamic color schemes
- [ ] Develop automated configuration and theme generation tools
- [ ] Port to other static site generators like Astro / Hugo
- [ ] Support for more custom UI components

---

## 🤝 Contributing

Contributions via Issues or Pull Requests are welcome, including but not limited to:
- Adding new UI components or visual effects
- Fixing known bugs or style conflicts
- Optimizing browser compatibility
- Improving documentation and translations

---

## 📄 License

This project is licensed under the [MIT License](./LICENSE).

---

## ❤️ Acknowledgements

- [Hexo Butterfly Theme](https://github.com/jerryc127/hexo-theme-butterfly): For providing an excellent thematic foundation.
- **Apple Design Language**: For design inspiration regarding Liquid Glass and spatial UI.
- **Material Design Community**: For references on Material You dark mode and dynamic colors.

---

<p align="center">
<strong>Made with ❤️ for Hexo Butterfly users.</strong>
</p>
