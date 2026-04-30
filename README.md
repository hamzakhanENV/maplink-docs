# Envitia MapLink Pro


<div class="row">
<div class="column" markdown=1>
Envitia's software technology for mission system developers, enabling them to create high performance geospatial intelligence, situational awareness and map-based systems. Feature rich and proven in demanding operational systems, Envitia's MapLink Pro provides system integrators and OEMs with the application control and flexibility they need while minimising delivery time and cost.
[Read more...](https://www.envitia.com/for-developers/maplink-pro/)

</div>
<div class="column">
<iframe width="560" height="315" src="https://www.youtube.com/embed/gDzkMZwUOow?si=5THKCqDyX_ZDglTm&amp;controls=0&amp;autoplay=1&amp;cc_load_policy=1&amp;mute=1&amp;loop=1&amp;playlist=gDzkMZwUOow" title="YouTube video player" frameborder="0" allow="autoplay;" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
</div>

<div class="row" markdown=1>


# Getting Started
## Installation
- [Get a trial version of MapLink Pro](https://forms.office.com/e/Lr7jN9TCC0).
- Our [Quick Start Guide](./pdf/MapLink Pro Quick Start Guide.pdf) will see you through the process of getting started.

## Samples
MapLink Pro comes installed with a variety of sample applications to get you started quickly.
You can also view our sample code and tips in our [GitHub repos](https://github.com/envitia).

## Platform Requirements
MapLink Pro has APIs for [C++](./api/cpp/) and [.Net](./api/dotnet/) and can be used on Windows and Linux.

## Resources
- [Envitia MapLink Pro API Documentation](./api/)
- [MapLink Studio Documentation](./studio/)
- [Support Pages](./pages/support/)
- [Licences](./licences)

# Docs
<ul>
    {% for item in site.data.docs.docs %}
    <li>
    <a href="{{ item.url | relative_url }}">{{ item.title }}</a>
    </li>
    {% endfor %}
    <li><a href="./pages/docs">All docs...</a></li>
</ul>



</div>

---

## Developer Site: UI Change Log

This section documents UI and structural changes made to the developer site for auditing purposes. Content changes to markdown pages are tracked via git history.

---

### Navigation overhaul
**Files:** `_layouts/default.html`, `_data/nav.yml`, `assets/js/nav.js`, `assets/css/style.scss`

Replaced the original shields.io badge-image navigation with a full HTML/CSS navigation bar:

- Sticky top nav bar fixed at the top of every page (`position: fixed`)
- Logo and site name on the left
- Dropdown menus for DOCS, API DOCS, RELEASES, and SUPPORT — each exposing sub-pages
- "REQUEST A TRIAL" rendered as a green call-to-action button
- Active section highlighting — the current nav item is highlighted based on the URL
- Mobile hamburger menu at viewports below 960px with tap-to-expand dropdowns
- Nav data driven by `_data/nav.yml`; add or reorder items there

---

### Search (Lunr.js)
**Files:** `search.json`, `assets/js/search.js`, `assets/css/style.scss`

Added client-side full-text search powered by [Lunr.js](https://lunrjs.com/):

- Search input in the top-right of the nav bar
- `search.json` is generated at build time by Jekyll — it indexes all pages that have a `title` in their frontmatter
- Results appear as a dropdown panel as the user types (minimum 2 characters)
- Matching text in page titles is highlighted in results
- Closes on Escape key or click outside
- Lunr.js loaded from unpkg CDN (`https://unpkg.com/lunr/lunr.js`)

---

### Version / announcement banner
**Files:** `_layouts/default.html`, `assets/css/style.scss`, `_data/nav.yml`

A slim green banner sits just below the nav bar, driven by the `messages:` list in `_data/nav.yml`. Features:

- Animated pulsing dot to draw attention
- Dismissible via the × button (client-side only — reappears on page reload)
- Update or remove entries in `_data/nav.yml` under `messages:` to control what is shown

---

### Breadcrumb trail
**Files:** `assets/js/breadcrumb.js`, `assets/css/style.scss`

Auto-generated breadcrumb displayed at the top of every content page, built from the URL path. The `pages/` directory segment is suppressed as it is structural, not meaningful to readers. Custom segment-to-label mappings are defined at the top of `breadcrumb.js`.

Example: `/pages/support/install-and-upgrade` renders as `Home › Support › Install & Upgrade`

---

### "Last updated" date
**Files:** `_layouts/default.html`, `assets/css/style.scss`

Pages can show a "Last updated" date by adding the following to their frontmatter:

```yaml
updated: "April 29, 2026"
```

No plugin required. If `updated:` is not present in the frontmatter, nothing is shown.

---

### On-page table of contents (TOC)
**Files:** `assets/js/toc.js`, `assets/css/style.scss`

A sticky "On this page" sidebar is generated automatically for any page containing 2 or more `h2`/`h3` headings:

- Appears as a right-hand sidebar on viewports wider than 1100px
- Scroll spy highlights the current section as the user scrolls
- Smooth scroll on click
- Hidden automatically on pages with fewer than 2 headings

---

### Copy button on code blocks
**Files:** `assets/js/copy-code.js`, `assets/css/style.scss`

A "Copy" button is injected into every `<pre>` code block. It:

- Appears on hover (always visible after copying)
- Uses the Clipboard API with a `document.execCommand` fallback for older browsers
- Shows "Copied!" confirmation for 2 seconds

---

### CSS architecture
**Files:** `assets/css/style.scss`

The original `@import "{{ site.theme }}"` (minimal theme CSS) was removed because its float-based layout conflicted with the new full-width design. All styles are now written from scratch in `style.scss`, using CSS custom properties (variables) for the Envitia brand colours:

| Variable | Value | Usage |
|---|---|---|
| `--green` | `#84bd00` | Primary brand green |
| `--green-dark` | `#6aa000` | Hover states, links |
| `--dark` | `#1f2a44` | Nav background, body text |
| `--dark-mid` | `#2d3d5e` | Mobile nav background |
| `--light` | `#f5f7fa` | Page background accents |

---

### Site-wide sidebar navigation panel
**Files:** `_layouts/default.html`, `assets/js/nav.js`, `assets/css/style.scss`

A slide-in "All Sections" panel accessible from every page via a sidebar icon button in the nav bar:

- Opens as a left-hand drawer below the nav bar without affecting the page layout
- Lists every top-level section from `_data/nav.yml`; sections with sub-pages show a `›` chevron button that expands the sub-menu independently of navigating to the section
- The section matching the current URL is automatically expanded and highlighted in solid green on load
- Closes on outside click, the × button, or the Escape key
- Works on all viewport sizes; on mobile a navigation link click also closes the panel

---

### Search keyboard navigation
**Files:** `assets/js/search.js`, `assets/css/style.scss`

Search results can now be navigated without a mouse:

- `↑` / `↓` arrow keys move the highlighted result up or down
- `Tab` / `Shift+Tab` cycle forward and backward through results
- `Enter` navigates to the currently highlighted result
- `Escape` closes the results panel and blurs the input
- The focused result is outlined in green so the selection is always visible

---

### Mobile search
**Files:** `_layouts/default.html`, `assets/js/search.js`, `assets/css/style.scss`

Search is now available on mobile viewports (≤ 960px). A dedicated search input appears at the top of the hamburger menu when it is opened:

- Styled to match the dark mobile nav theme
- Shares the same Lunr.js index as the desktop search — no additional build output required
- Results appear inline below the input within the nav dropdown
- Supports the same keyboard navigation and Escape behaviour as the desktop search
