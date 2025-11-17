# Ellty UI

A lightweight, interactive checkbox UI component built with **Alpine.js** and vanilla CSS. Demonstrates master–detail checkbox synchronization with a clean, modern design. Can be accessed live via: https://azhar25git.github.io

## Features

- ✅ **Master Checkbox Sync** — Toggle "All pages" to check/uncheck all page checkboxes instantly
- ✅ **Detail Sync** — Check individual pages; when all are checked, "All pages" auto-checks
- ✅ **Dynamic Loop** — Uses Alpine.js `x-for` to render page checkboxes from a data array (easy to add/remove pages)
- ✅ **Responsive Design** — Centered, card-like UI with custom-styled checkboxes
- ✅ **Alpine.js Reactive** — Two-way data binding with `x-model` and event handlers
- ✅ **Modern Styling** — Montserrat font, smooth hover effects, Material Design–inspired checkmarks

## Tech Stack

- **HTML5** — Semantic structure with Alpine.js directives
- **CSS3** — Flexbox layout, custom checkbox styling, SVG checkmark icons
- **Alpine.js 3.x** — Lightweight reactive framework (loaded via CDN)
- **Montserrat Font** — Google Fonts integration

## File Structure

```
.
├── index.html      # Main page with Alpine component
├── styles.css      # All styling (layout, checkboxes, buttons)
└── README.md       # This file
```

## Quick Start

1. **Open locally** — No build step needed!
   ```bash
   cd /path/to/uitest
   python3 -m http.server 8000
   ```
   Then visit `http://localhost:8000` in your browser.

2. **Test the sync logic**:
   - Click **"All pages"** → all 4 page checkboxes toggle together
   - Click any individual page → "All pages" auto-syncs if all are checked
   - Click "Done" button to submit (add logic as needed)

## How It Works

### Alpine Component (`checkboxSync()`)

```javascript
function checkboxSync() {
  return {
    allChecked: false,
    pages: [
      { id: 'page1', label: 'Page 1', checked: false },
      { id: 'page2', label: 'Page 2', checked: false },
      { id: 'page3', label: 'Page 3', checked: false },
      { id: 'page4', label: 'Page 4', checked: false },
    ],
    syncAll() {
      // Master checkbox → sync all pages
      this.pages.forEach(p => p.checked = this.allChecked);
    },
    syncMaster() {
      // Page checkbox → update master if all are checked
      this.allChecked = this.pages.every(p => p.checked === true);
    }
  };
}
```

**Key points:**
- `pages` is an array of objects with `id`, `label`, and `checked` state
- `syncAll()` runs when "All pages" changes → sets all `page.checked` to match `allChecked`
- `syncMaster()` runs when any page checkbox changes → sets `allChecked` to `true` only if **all** pages are checked

### Template Loop

```html
<template x-for="page in pages" :key="page.id">
  <label class="custom-checkbox">
    <span x-text="page.label"></span>
    <input type="checkbox" x-model="page.checked" @change="syncMaster()" />
    <span class="checkmark"></span>
  </label>
</template>
```

- `x-for="page in pages"` — Renders one label per page in the `pages` array
- `x-model="page.checked"` — Two-way bind the input to the page's `checked` state
- `@change="syncMaster()"` — Trigger sync logic on change

## Customization

### Add More Pages
Edit the `pages` array in the component:
```javascript
pages: [
  { id: 'page1', label: 'Page 1', checked: false },
  { id: 'page2', label: 'Page 2', checked: false },
  { id: 'page3', label: 'Page 3', checked: false },
  { id: 'page4', label: 'Page 4', checked: false },
  { id: 'page5', label: 'Page 5', checked: false },  // Add here
],
```

### Get Selected Pages
Add a method to retrieve selected pages:
```javascript
getSelected() {
  return this.pages.filter(p => p.checked).map(p => p.label);
}
```

### Pre-check Pages on Load
Set `checked: true` on any page:
```javascript
{ id: 'page2', label: 'Page 2', checked: true },
```

## Styling Details

- **Card container** — Flexbox column, centered with shadow and rounded corners
- **Custom checkboxes** — Hides native input, replaces with styled `<span class="checkmark">`
- **Checked state** — Blue background (`#2469f6`) with white SVG checkmark
- **Hover effects** — Smooth color transitions and box-shadow on hover
- **Button** — Yellow ("Done") with hover state for user feedback

## Browser Support

Works in all modern browsers supporting:
- ES6+ (Arrow functions, template literals)
- CSS Flexbox
- Alpine.js 3.x
- SVG (for checkmarks)

## License

Open source. Use freely in personal and commercial projects.

---

**Built with ❤️ using Alpine.js**
