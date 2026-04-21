# Power Apps UI Kit — @Awaji_PPF

> プリビルドコントロール集 & クイックフォームビルダー  
> Prebuilt controls library and quick form builder for Power Apps canvas apps.

---

## Overview

This is a single-page HTML tool built for Power Apps makers at **@Awaji PPF**. It combines two utilities in one interface, accessible via the top navigation tabs:

| Tab | Description |
|-----|-------------|
| **Controls** | Browse and copy prebuilt Power Apps controls with theme support |
| **フォームビルダー** | Visually build form layouts and export ready-to-use YAML + PowerFX |

---

## Tab 1 — Controls Library (コンポーネントライブラリ)

A showcase of prebuilt Power Apps controls. Each control card provides:

- **Live preview** rendered directly in the browser
- **6 color themes** switchable per card (Indigo, Emerald, Rose, Amber, Slate, Ocean)
- **Collapsible YAML panel** with syntax highlighting
- **One-click copy** to paste directly into a canvas app

### Available Controls

| Control | Type | Tag |
|---------|------|-----|
| Success Toast | `GroupContainer@1.5.0 · AutoLayout` | toast |
| DateTimePicker | PCF / Custom | date |
| ModernDataGrid | PCF / Custom | grid |
| Sidebar Navigation | `GroupContainer@1.5.0` | sidebar |
| *(more controls registered via `CanvasKit.registerControl()`)* | | |

### How to Use a Control

1. Open the page in a browser
2. Find the control card you want
3. Select a color theme using the dot picker in the card header
4. Click **"View YAML · Power Fx"** to expand the code panel
5. Click **Copy YAML** — paste directly into Power Apps Studio

### Theme System

Six built-in themes, each defined by a `primary`, `accent`, and `bg` color:

| Theme | Primary | Accent |
|-------|---------|--------|
| Indigo | `#4F46E5` | `#8B5CF6` |
| Emerald | `#059669` | `#10B981` |
| Rose | `#E11D48` | `#F43F5E` |
| Amber | `#D97706` | `#F59E0B` |
| Slate | `#1E293B` | `#475569` |
| Ocean | `#0284C7` | `#0EA5E9` |

Themes affect YAML output — `RGBA()` values in the generated code reflect the selected theme.

---

## Tab 2 — クイックフォームビルダー (Quick Form Builder)

A visual drag-and-drop builder for Power Apps modal forms. Design a form in the browser and export production-ready YAML and a `Patch()` formula.

### Features

- **Visual Builder** — real-time preview of the form layout
- **Generated Code** — switch to code view for YAML and PowerFX output
- **Field types:** Text Input, Dropdown, Date Picker
- **Drag-and-drop** reordering of fields
- **Edit modal** — customize label, placeholder, dropdown items, and required status
- **Settings panel** — configure form title, dimensions (px), button labels, SharePoint list name, and accent color
- **Control style toggle** — Classic Controls or Modern Controls YAML output
- **Copy buttons** for YAML and `Patch()` formula separately

### Workflow

```
1. Switch to the "フォームビルダー" tab
2. Add fields from the right panel (text / dropdown / date)
3. Edit field labels and options using the pencil icon
4. Adjust form settings (title, size, accent color, list name) in the "設定" panel
5. Switch to "生成されたコード" to see YAML and Patch formula
6. Copy and paste into Power Apps Studio
```

### Generated Output

**YAML** — A `conModalItems` GroupContainer with:
- `lblFormTitle` label
- `conLeft` and `conRight` containers (two-column layout)
- Individual field controls + label pairs, named systematically (e.g. `txtInput1`, `lblInput1`)
- `btnSubmit` and `btnCancel` buttons

**Patch Formula** — A `Patch()` expression pre-wired with all field variable references, ready to bind to a SharePoint list.

---

## Developer Notes

### Adding a New Control

Register a new control anywhere after the page scripts load:

```javascript
CanvasKit.registerControl({
  name: 'My Control',
  type: 'GroupContainer@1.5.0 · AutoLayout',
  tag: 'custom',
  renderPreview(theme) {
    // Return an HTMLElement or HTML string
    const el = document.createElement('div');
    el.textContent = 'Preview';
    return el;
  },
  buildYaml(theme) {
    // Return YAML string; use theme.primary, theme.accent, theme.bg
    return `- myControl:\n    Control: GroupContainer@1.5.0\n    ...`;
  }
});
```

### Project Structure

```
integrated.html        ← Single self-contained file (no dependencies)
├── <style>            ← index.html styles + .fb-wrapper scoped form builder styles
├── Ambient background ← Fixed decorative grid + blobs
├── Topbar             ← Logo, tab navigation, version pill
├── #tab-controls      ← Controls library panel (default active)
│   └── <main>         ← Control cards grid
├── #tab-formbuilder   ← Form builder panel
│   └── .fb-wrapper    ← Scoped form builder UI
│       ├── .left-pane ← Visual builder / Code view
│       └── .right-pane← Fields + Settings panels
├── Toast              ← Copy confirmation notification
└── <script>           ← CanvasKit + FormBuilder + switchTab()
```

### Key JavaScript APIs

| Function | Description |
|----------|-------------|
| `CanvasKit.registerControl(def)` | Register a new control card |
| `switchTab('controls' \| 'formbuilder')` | Switch the active page tab |
| `copyYaml(text)` | Copy text to clipboard + show toast |
| `addField(type)` | Add a field to the form builder |
| `renderCode()` | Re-generate YAML + Patch formula |
| `render()` | Re-render form preview + field list |

---

## Requirements

- Modern browser (Chrome, Edge, Firefox, Safari)
- No build step, no dependencies — open the `.html` file directly
- Clipboard API required for copy buttons (served over `https://` or `localhost`)

---

## Credits

Built for Power Apps makers · **@Awaji**  
YAML compatible with **Power Fx** · Canvas Apps
