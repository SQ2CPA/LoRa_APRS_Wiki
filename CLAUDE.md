# CLAUDE.md - LoRa APRS Wiki

## Project overview

Jekyll static site deployed on GitHub Pages at **wiki.lora-aprs.pl**. Documentation wiki for LoRa APRS projects (Tracker, Digi/iGate, Mobile App). Theme: Minimal Mistakes v4.24.0 (remote). Markdown processor: Kramdown.

## Architecture

### Sections

The site has 4 content sections, each in its own directory:

| Section | Directory | Layout | Sidebar |
|---------|-----------|--------|---------|
| General | `general/` | `general` | `_includes/sidebar/general.html` |
| Tracker | `lora_aprs_tracker/` | `tracker` | `_includes/sidebar/tracker.html` |
| Digi/iGate | `lora_aprs_digi/` | `digi` | `_includes/sidebar/digi.html` |
| Mobile App | `lora_aprs_mobile_app/` | `mobile_app` | `_includes/sidebar/mobile_app.html` |

Landing page (`index.md`) uses `default` layout with `_includes/sidebar/main.html`.

### How sidebars work

Each section has its own **manually maintained HTML sidebar** in `_includes/sidebar/`. The connection works as follows:

1. A markdown page declares `layout: tracker` in its frontmatter
2. Jekyll uses `_layouts/tracker.html` to render the page
3. The layout includes the sidebar: `{% include sidebar/tracker.html %}`
4. The sidebar contains a hard-coded `<nav>` with `<ul>/<li>/<a>` elements

**There is no auto-generation of sidebar navigation.** Every link must be added manually.

Sidebar HTML structure:
```html
<nav class="sidebar-nav">
    <h3>Section Title</h3>
    <ul>
        <li><a href="{{ '/' | relative_url }}">Go back</a></li>
        <li><a href="{{ '/section/page-name/' | relative_url }}">Page Title</a></li>
        <!-- more items -->
    </ul>
</nav>
```

All links use the `{{ '...' | relative_url }}` Jekyll filter for correct URL generation.

### Navigation layers

1. **Top header** (`_includes/header.html`) - always visible, links to 3 main projects
2. **Sidebar** (`_includes/sidebar/*.html`) - context-aware per section
3. **In-content links** - standard markdown links

## Adding a new page - checklist

### 1. Create the markdown file

Place it in the correct section directory, e.g. `lora_aprs_tracker/new-page.md`.

### 2. Add frontmatter

```yaml
---
layout: tracker
title: New Page Title
permalink: /lora_aprs_tracker/new-page/
---
```

**Critical rules:**
- `layout` must match the section (`tracker`, `digi`, `mobile_app`, `general`)
- `permalink` must follow the pattern `/<directory>/<slug>/` (with trailing slash)
- If layout is wrong, the page will render with the wrong sidebar (or no sidebar)

### 3. Add to sidebar

Edit `_includes/sidebar/tracker.html` (or the relevant section sidebar) and add:

```html
<li>
    <a href="{{ '/lora_aprs_tracker/new-page/' | relative_url }}">New Page Title</a>
</li>
```

Position the `<li>` where it makes sense in the navigation order.

### 4. Add images (if needed)

Place images in `assets/images/<project>/`. Use markdown to reference them:
```markdown
![Alt text](/assets/images/lora_aprs_tracker/screenshot.png)
```

## Common mistakes to avoid

- **Forgetting to update the sidebar** - the page will exist but be unreachable from navigation
- **Wrong layout in frontmatter** - page will show wrong section's sidebar
- **Missing trailing slash in permalink** - can cause 404s or redirect issues
- **Not using `relative_url` filter in sidebar links** - links may break if `baseurl` changes
- **Adding page to header.html when it should only be in sidebar** - header is for top-level sections only

## Key files

| File | Purpose |
|------|---------|
| `_config.yml` | Jekyll configuration, theme, plugins, permalink pattern |
| `_layouts/*.html` | Page templates (5 files, one per section + default) |
| `_includes/sidebar/*.html` | Sidebar navigation (5 files, manually maintained) |
| `_includes/header.html` | Top navigation bar |
| `_includes/footer.html` | Site footer |
| `assets/css/style.css` | All custom styles (SCSS), primary color `#0f9600` |

## Build & deploy

- **Deploy**: push to `main` branch, GitHub Pages builds automatically
- **Local dev**: `bundle exec jekyll serve` (requires Ruby + Jekyll)
- **Domain**: configured via `CNAME` file (wiki.lora-aprs.pl)
- **No npm/node/python dependencies** - pure Jekyll
