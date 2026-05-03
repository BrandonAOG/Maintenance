# AOG Maintenance Report — README

```markdown
# 🔧 AOG Maintenance Report

A single-page, mobile-first web form for **Always On Generators** field technicians.
Captures a complete generator maintenance visit — battery diagnostics, generator
condition, oil & filters, simulated outage test, gas system inspection, transfer
switch status, and mobile link connectivity — with auto-save, dark mode, and
one-tap PDF export.

> **Live Site:** https://brandonaog.github.io/Maintenance/

---

## 📸 Preview

```
┌─────────────────────────────────────────────┐
│  Always On Generators    Maintenance Report │
├─────────────────────────────────────────────┤
│  Customer & Job Info                        │
│  ┌──────────────┐  ┌──────────────────────┐ │
│  │   Battery    │  │     Generator        │ │
│  │  Condition   │  │  Startup / Coolant   │ │
│  │  CCA / SOH   │  │  Wiring / Interior   │ │
│  └──────────────┘  └──────────────────────┘ │
│  Oil & Filters                              │
│  Simulated Outage Test                      │
│  Gas System                                 │
│  Transfer Switch                            │
│  Other (Surge / Mobile Link / Signal)       │
└─────────────────────────────────────────────┘
```

---

## 📋 Form Sections

### Customer & Job Info
| Field | Detail |
|---|---|
| Name | Customer full name |
| Job # | Internal job reference |
| Date | Auto-fills to today on load |
| Address | Service location |
| Tech | Technician name |
| Model / Serial # | Generator model and serial |
| Hours | Current engine hour reading |

### Battery
| Field | Detail |
|---|---|
| Visual | Corrosion / Broken Cables / Good |
| Condition | Good / Average / Poor / Needs Replaced |
| Replaced | Y / N toggle |
| Voltage | Battery voltage reading |
| CCA | Cold Cranking Amps |
| SOH | State of Health % |
| Brand & Date | Battery manufacturer and install date |
| Water Level | Low / Full / Add |
| Notes | Free-text battery notes |

### Generator
| Field | Detail |
|---|---|
| Startup Test | Normal / Abnormal |
| Voltage | Generator output voltage |
| Case | Clean / Debris |
| Coolant Level | Full / 3/4 / 1/2 / Empty |
| Coolant Added | Ounces added |
| Wiring Check | Loose / Broken / Damaged / Good |
| Interior Check | Belts / Pulleys / Hoses / Harness |
| Overall Condition | Good / Average / Poor / Needs Replaced |
| Exercise Schedule | Day and time of weekly exercise run |
| Notes | Free-text generator notes |

### Oil & Filters
| Field | Detail |
|---|---|
| Oil Change Type | Full / Half |
| Filter Replaced | Y / N toggle |
| Filter Part # | Part number used |
| Notes | Free-text oil & filter notes |

### Simulated Outage Test
| Step | Captured |
|---|---|
| Generator Started Up | Y / N |
| Transferred to Generator Power | Y / N |
| Transferred Back to Line Power | Y / N |
| Generator Shut Down | Y / N |
| Voltage During Simulation | Text field |

### Gas System
| Field | Detail |
|---|---|
| Fuel Type | NG / LP |
| Tank Level | Text field |
| Leak Found | Y / N toggle |
| Visual Inspection | Rust / Shut-off Valve / Straps / Flex Connection / Regulator |
| Vented | Y / N toggle |
| Notes | Free-text gas system notes |

### Transfer Switch
| Field | Detail |
|---|---|
| TS Serial #1 | Serial number of first transfer switch |
| Condition #1 | Good / Avg / Poor / Needs Replaced |
| TS Serial #2 | Serial number of second transfer switch |
| Condition #2 | Good / Avg / Poor / Needs Replaced |
| Notes | Free-text transfer switch notes |

### Other
| Field | Detail |
|---|---|
| Surge Protection | Y / N |
| Green Light | Y / N |
| Monitor Ready | Y / N |
| Connected (Mobile Link) | Y / N |
| Signal % | Numeric signal strength |

---

## 🚀 Quick Start

```bash
git clone https://github.com/BrandonAOG/Maintenance.git
cd Maintenance
open index.html      # macOS
# Windows / Android — double-click index.html
```

No server, no build step, no dependencies to install.

---

## 🛠 Tech Stack

| Layer | Detail |
|---|---|
| **Framework** | None — Vanilla HTML / CSS / JS |
| **Fonts** | Google Fonts — Orbitron · Share Tech Mono · Exo 2 |
| **Storage** | Browser `localStorage` (auto-save draft) |
| **Hosting** | GitHub Pages |

---

## ✨ Features

### 🌓 Light / Dark Mode
- Defaults to system preference (`prefers-color-scheme`)
- Manual toggle button in the header, persisted to `localStorage`
- Light = professional white/amber industrial theme
- Dark = deep navy + neon cyan glow theme

### 📄 PDF Export
- One-tap browser print dialog
- Safari-specific guidance alert fires automatically on iOS/macOS Safari
- Forced light-mode styles injected at print time — dark mode never
  bleeds into printed output
- Single page layout with `overflow: hidden` to keep content on one
  `8.5 × 11in` sheet

### 💾 Auto-Save Draft
- All fields saved to `localStorage` every 30 seconds
- Also saves on every `change` and `input` event
- Draft restored automatically on next page load
- **Clear** button wipes both the form and the stored draft

### ✅ Y / N Radio Toggles
- Custom styled radio-button pairs for every Yes/No decision
- **Y selected** → green highlight
- **N selected** → red highlight
- Unselected → neutral gray outline

### ✅ Checkbox Groups
- Multi-select checkboxes styled as pill badges
- Checked state highlights with amber/cyan glow depending on theme

### 📅 Auto Date
- Date field pre-fills to today's date on page load
- Does not overwrite a restored draft date

---

## ⚙️ Configuration

### Changing the Home URL
```js
// In the toolbar button:
window.location.href = 'https://brandonaog.github.io/AOG-hub/'
```
Replace with your hub URL.

### Adding a Generator Condition Option
Locate the `gencond` radio group and add another `check-item`:
```html
<label class="check-item">
  <input type="radio" name="gencond" value="seized">
  <span>Seized</span>
</label>
```

### Adding a Gas Visual Inspection Item
Locate the `gasvisual` checkbox group:
```html
<label class="check-item">
  <input type="checkbox" name="gasvisual" value="corrosion">
  <span>Corrosion</span>
</label>
```

### Adding a Third Transfer Switch
Duplicate the TS Serial / Condition field rows in the
Transfer Switch section and change `tscond2` → `tscond3`,
`tsserial2` → `tsserial3`.

### Changing the Auto-Save Interval
```js
// Default is every 30 seconds
setInterval(saveDraft, 30000);
// Change 30000 to any millisecond value
```

### Logo
Loaded from a GitHub raw URL. Swap with any hosted image
or a `base64` data URI for fully offline operation:
```html
<img src="data:image/png;base64,YOUR_BASE64_HERE" ...>
```

---

## 🗂 File Structure

```
Maintenance/
├── index.html      ← Entire application (single self-contained file)
└── README.md       ← This file
```

---

## 📱 Device Compatibility

| Platform | Behavior |
|---|---|
| **Desktop** | Full two-column layout, hover states, print dialog |
| **iPad / Tablet** | Two-column layout, touch-friendly inputs |
| **iPhone / iOS Safari** | Single-column, auto-save draft, Safari print tip shown |
| **Android Chrome** | Single-column, auto-save draft, auto-download PDF |
| **Offline** | Fully functional after first browser load |

---

## 🖨 Print Layout Details

- Single sheet — `8.5 × 11in`, zero margins
- Dark mode automatically stripped to white before printing
- Toolbar, buttons, and theme toggle hidden
- Corner accent decorations preserved in amber
- All input fields render with bottom-border underlines only
- Textarea heights fixed for battery notes (60px) and gas/oil/TS notes (50px)
- Two-column grid maintained in print output

---

## 🔗 Related Repositories

| Repo | Description |
|---|---|
| [`AOG-hub`](https://github.com/BrandonAOG/AOG-hub) | Central Forms Hub dashboard |
| [`Installforms`](https://github.com/BrandonAOG/Installforms) | Electrical installation checklist |
| [`Generator-estimate-form`](https://github.com/BrandonAOG/Generator-estimate-form) | Estimate & quote form |
| [`Site-visit`](https://github.com/BrandonAOG/Site-visit) | Site inspection forms |
| [`Sketchpad`](https://github.com/BrandonAOG/Sketchpad) | Freehand field drawing tool |

---

## 📄 License

Internal business tool — © Always On Generators.  
Not licensed for redistribution.

---

## 👤 Author

**Brandon** — Always On Generators  
GitHub: [@BrandonAOG](https://github.com/BrandonAOG)
```

---

### Optional badges

```markdown
![HTML](https://img.shields.io/badge/HTML-Single--File-orange?style=flat-square&logo=html5)
![Vanilla JS](https://img.shields.io/badge/JS-Vanilla-yellow?style=flat-square&logo=javascript)
![Pages](https://img.shields.io/badge/Hosted-GitHub%20Pages-blue?style=flat-square&logo=github)
![Auto Save](https://img.shields.io/badge/Auto--Save-localStorage-green?style=flat-square)
![Mobile Ready](https://img.shields.io/badge/Mobile-iOS%20%2B%20Android-lightblue?style=flat-square&logo=apple)
![Print Ready](https://img.shields.io/badge/Print-Single%20Page%20PDF-red?style=flat-square&logo=adobeacrobatreader)
![Dark Mode](https://img.shields.io/badge/Theme-Light%20%2F%20Dark-purple?style=flat-square)
```
