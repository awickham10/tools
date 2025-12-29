# Tools Repository - Development Guide

This is a personal collection of single-page web applications hosted on GitHub Pages. Each tool is a self-contained HTML file with embedded CSS and JavaScript.

## Project Philosophy

- **Self-contained**: Each tool is a single HTML file with no external dependencies (except Google Fonts)
- **Aesthetic**: "Workshop Blueprint" theme - industrial, warm, crafted feel
- **Personal**: Not for mass-market use, but built with care and attention to detail
- **Functional**: Tools should work well on both mobile and desktop

---

## Repository Structure

```
tools/
├── index.html                    # Landing page (lists all tools)
├── CLAUDE.md                     # This file
├── README.md                     # Public documentation
├── [tool-name]/                  # Each tool in its own folder
│   └── index.html                # The tool (kebab-case folder names)
└── [another-tool]/
    └── index.html
```

### Naming Conventions

- **Folders**: kebab-case (e.g., `auto-loan-calculator`, `unit-converter`)
- **URLs**: Clean paths like `/tools/auto-loan-calculator/`
- **Titles**: Title Case in the UI (e.g., "Auto Loan Calculator")

---

## Design System

### Color Palette

All tools must use these CSS custom properties exactly:

```css
:root {
    /* Backgrounds - darkest to lightest */
    --bg-deep: #1a1915;           /* Page background */
    --bg-surface: #252320;        /* Card backgrounds */
    --bg-elevated: #2d2a26;       /* Elevated elements, results panels */
    --bg-input: #1f1e1a;          /* Input field backgrounds */

    /* Borders */
    --border-subtle: #3d3a35;     /* Default borders */
    --border-medium: #4a4640;     /* Emphasized borders, hover states */
    --border-focus: #e6a23c;      /* Focus rings (same as accent) */

    /* Text */
    --text-primary: #f5f0e6;      /* Main text, headings */
    --text-secondary: #a89f8c;    /* Descriptions, secondary info */
    --text-muted: #6b6358;        /* Labels, placeholders, hints */

    /* Accent - Amber (primary interactive color) */
    --accent-amber: #e6a23c;      /* Primary accent */
    --accent-amber-dim: #b8832f;  /* Darker amber for gradients */
    --accent-amber-glow: rgba(230, 162, 60, 0.15);  /* Focus glow, subtle backgrounds */

    /* Semantic colors (use sparingly) */
    --accent-green: #4ade80;      /* Success states */
    --accent-green-dim: #22c55e;
    --accent-red: #f87171;        /* Error states */
    --accent-red-dim: #ef4444;

    /* Blueprint grid (background effect) */
    --grid-color: rgba(230, 162, 60, 0.06);   /* Fine grid lines */
    --grid-accent: rgba(230, 162, 60, 0.12);  /* Major grid lines */
}
```

### Typography

**Font Stack** (load from Google Fonts):

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700&family=Source+Serif+4:opsz,wght@8..60,400;8..60,500&display=swap" rel="stylesheet">
```

**Usage:**

| Element | Font | Weight | Size | Style |
|---------|------|--------|------|-------|
| Page title (h1) | JetBrains Mono | 700 | 1.75rem (tool) / 2.5rem (landing) | uppercase on landing |
| Section titles | JetBrains Mono | 600 | 0.7rem | uppercase, letter-spacing: 0.1em |
| Labels | JetBrains Mono | 500 | 0.75rem | normal |
| Input values | JetBrains Mono | 400 | 0.95rem | normal |
| Body text / descriptions | Source Serif 4 | 400 | 0.9-1rem | normal |
| Small text / hints | JetBrains Mono | 400 | 0.65-0.75rem | normal |

**Key principle**: JetBrains Mono for all UI elements (labels, values, buttons). Source Serif 4 for descriptive body text only.

### Spacing Scale

Use consistent spacing throughout:

- `4px` - Tight spacing (gaps in toggles)
- `8px` - Small spacing (label margins, small gaps)
- `12px` - Medium-small (padding in compact elements)
- `16px` - Medium (standard gaps, margins)
- `20px` - Medium-large (section padding, input group margins)
- `24px` - Large (content padding mobile, card padding)
- `32px` - Extra large (content padding desktop, major gaps)

### Border Radius

- `8px` - Inputs, buttons, small cards, icons
- `12px` - Result panels, inner cards
- `16px` - Main calculator/tool cards

---

## Core Components

### Blueprint Background

Every page must include this as the first child of `<body>`:

```html
<div class="blueprint-bg"></div>
```

```css
.blueprint-bg {
    position: fixed;
    inset: 0;
    background-image:
        linear-gradient(var(--grid-color) 1px, transparent 1px),
        linear-gradient(90deg, var(--grid-color) 1px, transparent 1px),
        linear-gradient(var(--grid-accent) 1px, transparent 1px),
        linear-gradient(90deg, var(--grid-accent) 1px, transparent 1px);
    background-size:
        20px 20px,
        20px 20px,
        100px 100px,
        100px 100px;
    pointer-events: none;
    opacity: 0.8;
}
```

### Page Header (Tool Pages)

Every tool page must have a back link and header:

```html
<div class="header">
    <a href="../" class="back-link">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M19 12H5M12 19l-7-7 7-7"/>
        </svg>
        Back to Tools
    </a>
    <h1>Tool Name Here</h1>
    <p>Brief description of what the tool does</p>
</div>
```

```css
.header {
    margin-bottom: 32px;
    animation: fadeIn 0.5s ease-out;
}

.back-link {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    font-weight: 500;
    color: var(--text-muted);
    text-decoration: none;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin-bottom: 16px;
    transition: color 0.2s;
}

.back-link:hover {
    color: var(--accent-amber);
}

.back-link svg {
    width: 14px;
    height: 14px;
    transition: transform 0.2s;
}

.back-link:hover svg {
    transform: translateX(-3px);
}

.header h1 {
    font-family: 'JetBrains Mono', monospace;
    font-size: 1.75rem;
    font-weight: 700;
    letter-spacing: -0.02em;
    color: var(--text-primary);
    margin-bottom: 4px;
}

.header p {
    color: var(--text-secondary);
    font-size: 1rem;
}
```

### Section Titles

Used to label groups of inputs or results:

```html
<div class="section-title">Inputs</div>
```

```css
.section-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    font-weight: 600;
    color: var(--accent-amber);
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
}

.section-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border-subtle);
}
```

### Input Fields

**Basic input with prefix (currency):**

```html
<div class="input-group">
    <label>Vehicle Price</label>
    <div class="input-wrapper has-prefix">
        <span class="prefix">$</span>
        <input type="number" id="vehicle-price" value="35000" oninput="calculate()">
    </div>
</div>
```

**Input with suffix (percentage):**

```html
<div class="input-group">
    <label>Interest Rate</label>
    <div class="input-wrapper has-suffix">
        <input type="number" id="rate" value="6.5" step="0.1">
        <span class="suffix">%</span>
    </div>
</div>
```

```css
.input-group {
    margin-bottom: 20px;
}

.input-group label {
    display: block;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    font-weight: 500;
    color: var(--text-secondary);
    margin-bottom: 8px;
}

.input-wrapper {
    position: relative;
}

.input-wrapper .prefix,
.input-wrapper .suffix {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.85rem;
    color: var(--text-muted);
    pointer-events: none;
}

.input-wrapper .prefix { left: 14px; }
.input-wrapper .suffix { right: 14px; }

.input-wrapper input[type="number"],
.input-wrapper input[type="text"] {
    width: 100%;
    padding: 12px 14px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.95rem;
    color: var(--text-primary);
    background: var(--bg-input);
    border: 1px solid var(--border-subtle);
    border-radius: 8px;
    outline: none;
    transition: all 0.2s;
    -moz-appearance: textfield;
}

/* Hide number spinners */
.input-wrapper input[type="number"]::-webkit-outer-spin-button,
.input-wrapper input[type="number"]::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

.input-wrapper input:focus {
    border-color: var(--accent-amber);
    box-shadow: 0 0 0 3px var(--accent-amber-glow);
}

.input-wrapper.has-prefix input { padding-left: 32px; }
.input-wrapper.has-suffix input { padding-right: 60px; }
```

### Sliders (Range Inputs)

For inputs that benefit from a slider:

```html
<div class="input-group">
    <label>Interest Rate (APR)</label>
    <div class="input-wrapper has-suffix">
        <input type="number" id="rate" value="6.5" step="0.1" oninput="syncSlider('rate')">
        <span class="suffix">%</span>
    </div>
    <div class="slider-container">
        <input type="range" id="rate-slider" min="0" max="20" step="0.1" value="6.5" oninput="syncInput('rate')">
        <div class="slider-labels">
            <span>0%</span>
            <span>20%</span>
        </div>
    </div>
</div>
```

```css
.slider-container {
    margin-top: 10px;
}

.slider-container input[type="range"] {
    width: 100%;
    height: 4px;
    border-radius: 2px;
    background: var(--border-subtle);
    outline: none;
    -webkit-appearance: none;
    cursor: pointer;
}

.slider-container input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 16px;
    height: 16px;
    border-radius: 50%;
    background: var(--accent-amber);
    cursor: pointer;
    box-shadow: 0 2px 8px rgba(230, 162, 60, 0.4);
    transition: transform 0.15s, box-shadow 0.15s;
}

.slider-container input[type="range"]::-webkit-slider-thumb:hover {
    transform: scale(1.15);
    box-shadow: 0 2px 12px rgba(230, 162, 60, 0.5);
}

.slider-container input[type="range"]::-moz-range-thumb {
    width: 16px;
    height: 16px;
    border: none;
    border-radius: 50%;
    background: var(--accent-amber);
    cursor: pointer;
}

.slider-labels {
    display: flex;
    justify-content: space-between;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: var(--text-muted);
    margin-top: 6px;
}
```

### Mode Toggle (Tab Buttons)

For tools with multiple modes/views:

```html
<div class="mode-toggle">
    <button class="active" onclick="setMode('mode1')">Mode One</button>
    <button onclick="setMode('mode2')">Mode Two</button>
</div>
```

```css
.mode-toggle {
    display: flex;
    background: var(--bg-deep);
    border-bottom: 1px solid var(--border-subtle);
    padding: 4px;
    gap: 4px;
}

.mode-toggle button {
    flex: 1;
    padding: 12px 16px;
    border: none;
    background: transparent;
    border-radius: 8px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.8rem;
    font-weight: 500;
    color: var(--text-muted);
    cursor: pointer;
    transition: all 0.2s;
}

.mode-toggle button:hover:not(.active) {
    color: var(--text-secondary);
    background: var(--bg-surface);
}

.mode-toggle button.active {
    background: var(--accent-amber);
    color: var(--bg-deep);
    font-weight: 600;
}
```

### Results Display

```html
<div class="results">
    <div class="result-row">
        <span class="label">Total Amount</span>
        <span class="value" id="total">$0</span>
    </div>
    <div class="result-row highlight-row">
        <span class="label">Monthly Payment</span>
        <span class="value" id="monthly">$0</span>
    </div>
</div>
```

```css
.results {
    background: var(--bg-elevated);
    border: 1px solid var(--border-subtle);
    border-radius: 12px;
    padding: 20px;
}

.result-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 0;
    border-bottom: 1px solid var(--border-subtle);
}

.result-row:last-child {
    border-bottom: none;
}

.result-row .label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    color: var(--text-muted);
}

.result-row .value {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.9rem;
    font-weight: 600;
    color: var(--text-primary);
}

/* Highlighted result (the main output) */
.result-row.highlight-row {
    background: linear-gradient(135deg, var(--accent-amber), var(--accent-amber-dim));
    margin: 16px -20px -20px -20px;
    padding: 16px 20px;
    border-radius: 0 0 11px 11px;
    border-bottom: none;
}

.result-row.highlight-row .label,
.result-row.highlight-row .value {
    color: var(--bg-deep);
    font-weight: 600;
}
```

### Main Tool Card

Wrap the tool's content in a card:

```html
<div class="tool-card">
    <!-- Mode toggle if needed -->
    <div class="content">
        <!-- Tool content here -->
    </div>
</div>
```

```css
.tool-card {
    background: var(--bg-surface);
    border: 1px solid var(--border-subtle);
    border-radius: 16px;
    overflow: hidden;
    animation: fadeIn 0.5s ease-out 0.1s both;
}

.content {
    padding: 24px;
}

@media (min-width: 768px) {
    .content {
        padding: 32px;
    }
}
```

---

## Animations

### Standard Animations

```css
@keyframes fadeIn {
    from { opacity: 0; transform: translateY(-10px); }
    to { opacity: 1; transform: translateY(0); }
}

@keyframes slideIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}

@keyframes fadeSlideIn {
    from { opacity: 0; transform: translateY(-20px); }
    to { opacity: 1; transform: translateY(0); }
}
```

### Animation Usage

- **Page header**: `animation: fadeIn 0.5s ease-out`
- **Main card**: `animation: fadeIn 0.5s ease-out 0.1s both`
- **Content sections**: `animation: slideIn 0.4s ease-out 0.15s both`
- **Staggered elements**: Increment delay by `0.05s` for each element

### Hover Transitions

Standard transition timing:
- Quick interactions (color, opacity): `0.2s ease`
- Transforms (scale, translate): `0.15s ease` or `0.25s ease`
- Complex state changes: `0.3s ease`

---

## Responsive Design

### Breakpoints

- **Mobile**: < 768px (default styles)
- **Tablet/Desktop**: >= 768px (`@media (min-width: 768px)`)
- **Large desktop**: >= 1024px (optional, for extra polish)

### Mobile-First Approach

Write mobile styles first, then enhance for larger screens:

```css
/* Mobile (default) */
.content {
    padding: 24px;
}

/* Desktop */
@media (min-width: 768px) {
    .content {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 32px;
        padding: 32px;
    }
}
```

### Common Mobile Adjustments

```css
@media (max-width: 767px) {
    body {
        padding: 16px 12px 32px;
    }

    .header h1 {
        font-size: 1.5rem;
    }

    .mode-toggle button {
        font-size: 0.7rem;
        padding: 10px 12px;
    }
}
```

---

## Adding a New Tool

### Step 1: Create the folder and file

```bash
mkdir [tool-name]
touch [tool-name]/index.html
```

### Step 2: Use this template

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tool Name</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700&family=Source+Serif+4:opsz,wght@8..60,400;8..60,500&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-deep: #1a1915;
            --bg-surface: #252320;
            --bg-elevated: #2d2a26;
            --bg-input: #1f1e1a;
            --border-subtle: #3d3a35;
            --border-medium: #4a4640;
            --border-focus: #e6a23c;
            --text-primary: #f5f0e6;
            --text-secondary: #a89f8c;
            --text-muted: #6b6358;
            --accent-amber: #e6a23c;
            --accent-amber-dim: #b8832f;
            --accent-amber-glow: rgba(230, 162, 60, 0.15);
            --grid-color: rgba(230, 162, 60, 0.06);
            --grid-accent: rgba(230, 162, 60, 0.12);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        html { font-size: 16px; }

        body {
            font-family: 'Source Serif 4', Georgia, serif;
            background: var(--bg-deep);
            min-height: 100vh;
            color: var(--text-primary);
            line-height: 1.6;
            padding: 24px 16px 48px;
        }

        /* Blueprint grid background */
        .blueprint-bg {
            position: fixed;
            inset: 0;
            background-image:
                linear-gradient(var(--grid-color) 1px, transparent 1px),
                linear-gradient(90deg, var(--grid-color) 1px, transparent 1px),
                linear-gradient(var(--grid-accent) 1px, transparent 1px),
                linear-gradient(90deg, var(--grid-accent) 1px, transparent 1px);
            background-size: 20px 20px, 20px 20px, 100px 100px, 100px 100px;
            pointer-events: none;
            opacity: 0.8;
        }

        .container {
            position: relative;
            max-width: 1000px;
            margin: 0 auto;
        }

        /* === PASTE COMPONENT STYLES FROM ABOVE === */

        /* Add tool-specific styles here */

    </style>
</head>
<body>
    <div class="blueprint-bg"></div>

    <div class="container">
        <div class="header">
            <a href="../" class="back-link">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M19 12H5M12 19l-7-7 7-7"/>
                </svg>
                Back to Tools
            </a>
            <h1>Tool Name</h1>
            <p>Brief description</p>
        </div>

        <div class="tool-card">
            <!-- Tool content here -->
        </div>
    </div>

    <script>
        // Tool logic here
    </script>
</body>
</html>
```

### Step 3: Add to landing page

Edit `index.html` and add a new card to `.tools-grid`:

```html
<a href="[tool-name]/" class="tool-card">
    <div class="tool-card-icon">
        <svg viewBox="0 0 24 24" fill="none" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
            <!-- Icon path here - use Lucide icons or similar -->
        </svg>
    </div>
    <h2>Tool Name</h2>
    <p>Brief description of what the tool does and why it's useful.</p>
    <span class="tool-card-action">
        Open
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M5 12h14M12 5l7 7-7 7"/>
        </svg>
    </span>
</a>
```

### Step 4: Update README.md

Add the new tool to the "Available Tools" list.

---

## Code Conventions

### HTML

- Use semantic HTML where appropriate
- IDs for elements that need JavaScript access
- Classes for styling
- `oninput` for real-time calculation updates

### CSS

- All colors via CSS custom properties (never hardcode)
- Mobile-first responsive design
- Logical property order: positioning, display, box model, typography, visual, animation
- Comment major sections

### JavaScript

- Vanilla JS only (no frameworks)
- Cache DOM elements at the top
- Use `const` and `let` (never `var`)
- Descriptive function names
- Format numbers for display (use `toLocaleString()`)

### Formatting Helper

```javascript
function formatCurrency(amount) {
    const sign = amount < 0 ? '-' : '';
    return sign + '$' + Math.abs(Math.round(amount)).toLocaleString('en-US');
}

function formatPercent(value, decimals = 1) {
    return value.toFixed(decimals) + '%';
}

function formatNumber(value, decimals = 0) {
    return Number(value.toFixed(decimals)).toLocaleString('en-US');
}
```

---

## Checklist for New Tools

Before considering a tool complete:

- [ ] Uses all CSS custom properties (no hardcoded colors)
- [ ] Includes blueprint background
- [ ] Has back link to landing page
- [ ] Header with h1 and description
- [ ] Responsive on mobile and desktop
- [ ] Inputs have labels
- [ ] Focus states on interactive elements (amber glow)
- [ ] Animations on page load
- [ ] Hover states on interactive elements
- [ ] Results are clearly displayed
- [ ] Primary result is highlighted (amber gradient row)
- [ ] Added to landing page with icon and description
- [ ] Added to README.md
- [ ] Tested in browser (both mobile and desktop viewport)

---

## Icon Resources

For tool card icons, use simple line icons. Good sources:
- [Lucide Icons](https://lucide.dev/) - Recommended, consistent style
- [Feather Icons](https://feathericons.com/)

Icon guidelines:
- Use `viewBox="0 0 24 24"`
- `stroke-width="1.5"` for tool icons
- `stroke-linecap="round" stroke-linejoin="round"`
- No fill, stroke only
