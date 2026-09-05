# Hexo Butterfly Glass

[中文版](README.md)

**Current release: v2.1.1** · [Changelog](CHANGELOG.md)

A modular Liquid Glass / Glassmorphism enhancement system for the Hexo Butterfly theme.

This project does not modify Butterfly source code. It uses independent CSS modules, a small runtime script, and Hexo injection configuration to add Light/Dark glass materials, CSS ambient environment lighting, background transmission, depth, responsive behavior, and page-specific controls.

## Current Architecture

### Glass Environment

The environment is built from broad, low-saturation CSS fields instead of a plain white or black background.

- Light mode uses soft blue, violet, and warm fields.
- Dark mode uses deep gray with blue, violet, and subtle cyan light.
- Butterfly 5.7.0 uses `body` as the actual background container; `#web_bg` remains as a compatibility selector.
- Mobile mode reduces fixed backgrounds and blur cost.

### Surface Hierarchy

```text
Environment
    ↓
Primary Glass Surface
    ↓
Transparent Content Layer
```

For article pages, `#post` is the primary Glass Surface and `#article-container` is a transparent content layer. Body content, code blocks, tags, and share controls do not create another `backdrop-filter` context. Shuoshuo has no `#post` wrapper, so each `.shuoshuo-item` receives its own Glass Surface.

### Controls and Runtime

- The author card and Follow Me button support both themes.
- WeChat, QQ, and other share controls use a quiet edge highlight instead of a large optical fill.
- `js/glass-runtime.js` detects browser capabilities and manages Full, Reduced, Fallback, Disabled, mobile, and reduced-motion states.

### v2.1.0 Navigation Coverage

- The mobile `#sidebar #sidebar-menus` drawer is now a complete independent Glass Surface.
- The inner `.menus_items` layer is transparent instead of keeping Butterfly's solid menu card.
- The top navigation `.menus_item_child` dropdown is now an independent glass menu surface.
- The mobile drawer and dropdown menu support both Light and Dark themes.
- `lg-disabled` and `lg-fallback` turn off expensive blur while keeping readable fallback backgrounds.
- No new JavaScript is required, and Butterfly source files are not modified.

This update is contained in:

```text
css/glass-navbar.css
css/glass-responsive.css
```

## Project Structure

```text
butterfly-glass/
├── css/
│   ├── glass-tokens.css        # Design tokens and theme variables
│   ├── glass-environment.css   # Page environment and ambient light
│   ├── glass-core.css          # Core Glass Surface primitive
│   ├── glass-optical.css       # Optical highlights and pointer light
│   ├── glass-depth.css         # Elevation and depth
│   ├── glass-archive.css       # Archive page
│   ├── glass-post.css          # Article hierarchy and reading layer
│   ├── glass-page.css          # Shuoshuo and author controls
│   ├── glass-responsive.css    # Mobile / Tablet / Desktop rules
│   ├── glass-navbar.css        # Floating navigation
│   ├── glass-tag.css           # Tags and share controls
│   ├── glass-toc.css           # Table of contents
│   └── glass-search.css        # Search dialog
├── js/
│   └── glass-runtime.js        # Capability and performance runtime
├── config_butterfly_glass.yml  # Optional configuration example
├── glass-state.json            # State record
├── README.md                   # Default Chinese documentation
├── README_EN.md                # English documentation
└── CHANGELOG.md                # Version history
```

## Installation

Copy `butterfly-glass/` into the `source/` directory of your Hexo site:

```text
Your-Hexo-Site/
├── _config.butterfly.yml
└── source/
    └── butterfly-glass/
```

Add the files to Butterfly's `_config.butterfly.yml` in this order:

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

`glass-tokens.css` must be loaded first. Removing it leaves all `--lg-*` variables undefined.

### Upgrade from v2.0

The recommended upgrade is to replace the complete `butterfly-glass/` directory with the v2.1 directory while keeping your own `_config.butterfly.yml`.

If you only need the fixes in this release, replace at least:

```text
source/butterfly-glass/css/glass-navbar.css
source/butterfly-glass/css/glass-responsive.css
```

Do not rename the directory to `butterfly-glass-v4/`, `butterfly-glass-v5/`, or another versioned name.

## Runtime Configuration

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

Supported `reducedMode` values are `auto`, `full`, `reduced`, and `fallback`.

## Development and Verification

```bash
npm install
npx hexo generate
npx hexo server
```

Target environment:

- Hexo 8.1.2
- Butterfly 5.7.0
- Modern Chrome, Edge, Firefox, and Safari
- Desktop and Mobile
- Light and Dark themes

Verified page types include Home, Archive, Article, Shuoshuo, and custom pages. The checks cover article Surface Hierarchy, dynamic Shuoshuo items, Light/Dark controls, quiet share buttons, and mobile Reduced Glass.

The v2.1 checks also cover the mobile glass drawer, the transparent inner menu layer, and the top navigation glass dropdown.

### v2.1.1 Dropdown Alignment Fix

- Fixed the desktop pointer path from the “Resource Sources” trigger to its dropdown items.
- Preserved Butterfly’s transparent bridge above the dropdown so the menu does not close while the pointer travels into it.
- Centered the floating Glass dropdown relative to its trigger instead of relying on right alignment.
- Unified the width of all four options so the hover surface stays inside the Glass menu.
- Removed the duplicated Butterfly `li:hover` background from the Glass option state.
- Kept Light / Dark, fallback, and mobile behavior unchanged without modifying Butterfly source files.

This release updates:

```text
css/glass-navbar.css
```

## Release Summary

- Rebuilt the Glass Environment and bound it to the actual Butterfly `body` background.
- Established the `#post` / `#article-container` Surface Hierarchy.
- Fixed the `glass-navbar.css` and runtime asset paths.
- Added `glass-page.css` for Shuoshuo and author-card controls.
- Reworked the Follow Me button for Light and Dark themes.
- Split article tags from Share.js controls.
- Reduced highlights and shadows on dark-mode tags, WeChat, and QQ controls.
- Added unified radius and responsive performance rules.
- Removed obsolete legacy CSS and runtime files from the repository root.
- Passed Hexo generation and browser checks.

If old styles remain after an update, run `npx hexo clean`, generate again, restart the server, and hard-refresh the browser.

When the page becomes transparent or variables appear to be missing, check in this order:

```text
Does glass-tokens.css exist?
        ↓
Can /butterfly-glass/css/glass-tokens.css be loaded directly?
        ↓
Are the --lg-* variables defined?
        ↓
Only then inspect module selectors and theme overrides.
```

## Final Files

```text
css/glass-tokens.css
css/glass-environment.css
css/glass-core.css
css/glass-optical.css
css/glass-depth.css
css/glass-archive.css
css/glass-post.css
css/glass-page.css
css/glass-responsive.css
css/glass-navbar.css
css/glass-tag.css
css/glass-toc.css
css/glass-search.css
js/glass-runtime.js
config_butterfly_glass.yml
glass-state.json
README.md
README_EN.md
CHANGELOG.md
```

The project directory must remain `butterfly-glass/`. Do not rename it to a versioned directory such as `butterfly-glass-v4/` or `butterfly-glass-v5/`.

## Design Principles

- Enhance, don't replace.
- One visual region should normally have one primary Glass Surface.
- Content inside Glass should not use another `backdrop-filter` by default.
- Let the Environment provide material variation.
- Do not simulate glass by endlessly increasing opacity or blur.
- Do not modify Butterfly source code.
- Visual effects must support reading and navigation.

## License

MIT License

## Credits

- [Hexo](https://hexo.io/)
- [Butterfly Theme](https://github.com/jerryc127/hexo-theme-butterfly)
- Apple Liquid Glass / visionOS design language
- Material Design / Material You
