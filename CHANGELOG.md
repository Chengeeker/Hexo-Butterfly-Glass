# Changelog

All notable changes to Hexo Butterfly Glass are documented here.

## [2.1.0] - 2026-09-05

Version 2.1 is a focused coverage and usability update on top of the v2.0 Glass System. It fixes the remaining Butterfly navigation surfaces that were still using the original theme backgrounds.

### Navigation coverage

- Added a complete Glass Surface for the mobile `#sidebar #sidebar-menus` drawer.
- Made the inner mobile `.menus_items` layer transparent instead of keeping Butterfly's solid menu card.
- Added an independent glass surface for the top navigation `.menus_item_child` dropdown.
- Added Light and Dark theme styling for both surfaces, including readable text and quiet edge highlights.

### Performance and fallback

- Kept the mobile drawer and top dropdown as the only new independent blur contexts.
- Added `lg-disabled` and `lg-fallback` handling so unsupported or reduced environments can remove blur safely.
- Did not add JavaScript and did not modify Butterfly source files.

### Documentation and release

- Expanded the Chinese and English README instructions for installation, upgrade, rebuild, and browser verification.
- Documented the exact selectors and the v2.0 → v2.1 upgrade path.
- Added a release archive containing the complete `butterfly-glass/` directory.

### Verification

- Tested the local Hexo 8.1.2 / Butterfly 5.7.0 blog on Mobile Light and Dark sidebar states.
- Tested the local Hexo 8.1.2 / Butterfly 5.7.0 game site on Desktop Light and Dark dropdown states.
- Confirmed that sidebar menu content and dropdown links remain readable.

## [2.0.0] - 2026-08-24

Version 2.0 is a structural and visual upgrade from the 1.1 release. It moves the project from a collection of component overrides to a modular Glass System with an explicit environment, surface hierarchy, runtime states, and responsive performance rules.

### Highlights

- Introduced a real CSS Glass Environment behind the UI surfaces.
- Rebuilt the Light and Dark material parameters independently.
- Established a clear `Environment → Primary Surface → Content` hierarchy.
- Removed unnecessary nested Glass and repeated `backdrop-filter` contexts.
- Added a dedicated page layer for Shuoshuo and author-card controls.
- Added bilingual documentation with Chinese as the default README.
- Removed obsolete 1.1-era files from the repository root.

### Visual System

- Added `glass-tokens.css` as the central design-token layer.
- Added dedicated Light / Dark surface, border, highlight, shadow, radius, and motion variables.
- Added `glass-environment.css` with broad, low-saturation ambient fields.
- Bound the environment to the actual Butterfly 5.7.0 `body` background container.
- Added a unified radius system from small controls to large page surfaces.
- Preserved optical highlights and depth while reducing unnecessary visual noise.

### Surface Hierarchy

- Made `#post` the primary article Glass Surface.
- Changed `#article-container` into a transparent content layer.
- Disabled nested `backdrop-filter` for article content, code blocks, and internal content surfaces.
- Kept Archive, recent-post cards, sidebar cards, and floating controls as independent surfaces only where appropriate.
- Added Glass surfaces for dynamically rendered `.shuoshuo-item` blocks, which are not wrapped by `#post`.

### Article Controls

- Split article tags from Share.js controls.
- Added support for Butterfly's actual `.post-meta__tags` selector.
- Reduced the strong gradients, inset highlights, and shadows used by the 1.1 tag/share treatment.
- WeChat, QQ, and other share controls now use quiet translucent fills with edge highlights.
- Dark-mode tags and share controls no longer look like heavily illuminated plastic buttons.

### Author Card and Floating Controls

- Reworked the homepage Follow Me button into a theme-aware Glass child control.
- Added Light-mode dark icon/text contrast.
- Added Dark-mode light icon/text contrast.
- Preserved the author card as a primary surface while keeping its button as a quieter child layer.
- Unified floating control radius, border, shadow, and icon treatment.

### Runtime and Performance

- Fixed the runtime asset path to `/butterfly-glass/js/glass-runtime.js`.
- Added consistent `lg-*` runtime state classes alongside compatibility classes.
- Added explicit `lg-disabled` handling.
- Added mobile Full Glass state handling through `lg-mobile-full`.
- Preserved automatic Reduced Glass on mobile by default.
- Preserved `prefers-reduced-motion` handling.
- Kept pointer-driven optical updates limited to fine-pointer devices.

### Compatibility and Maintenance

- Fixed the incorrect `glass-navbar.css.css` injection path.
- Replaced obsolete variable references in the search module.
- Kept `glass-tokens.css` as the first required stylesheet.
- Kept the project directory name fixed as `butterfly-glass/`.
- Did not modify Butterfly theme source files.
- Removed obsolete files from the repository root:

  ```text
  css/glass-ambient.css
  css/glass-background.css
  css/glass-config.css
  css/glass-variable.css
  css/glass.css
  js/glass-config.js
  ```

### Verification

- Hexo 8.1.2 build passed.
- Butterfly 5.7.0 build passed.
- Checked Home, Archive, Article, Shuoshuo, and custom pages.
- Checked Light and Dark themes.
- Checked Desktop and Mobile layouts.
- Confirmed article content does not create nested Glass surfaces.
- Confirmed dynamically rendered Shuoshuo items receive the new Glass surface.

## [1.1.0]

The 1.1 release established the first Liquid Glass direction for Butterfly, including early component-level glass overrides, floating navigation, tag styling, search styling, and initial runtime/configuration experiments.

Version 2.0 keeps the visual direction but replaces the old scattered override approach with a more maintainable modular system.

## Upgrade Guide: 1.1 → 2.0

1. Replace the old `css/` and `js/` files with the v2.0 files.
2. Ensure `glass-tokens.css` is loaded first.
3. Add `glass-page.css` to the injection order.
4. Use `/butterfly-glass/js/glass-runtime.js` as the runtime path.
5. Remove references to the deleted legacy files.
6. Keep the installation directory named `butterfly-glass/`.
7. Clear Hexo's generated output before checking the new version:

   ```bash
   hexo clean
   hexo generate
   hexo server
   ```
