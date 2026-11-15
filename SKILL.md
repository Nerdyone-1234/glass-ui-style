---
name: glass-ui-style
description: Apple-inspired website style with glassmorphism, dark mode, an electric-cyan accent, spring animations and fluid typography. Use when building or restyling a web page or UI in this glass style, or when /glass-ui-style is invoked.
---

# Glass UI Style — Apple-inspired glassmorphism

This skill describes the exact patterns, tokens and workflow for pages in this style: refined Apple-inspired design, a deep-space dark mode, electric cyan as the brand color, real glassmorphism, spring physics and fluid typography.

---

## 1. Design token system

All values live in `:root` as CSS custom properties. **Never hard-code colors, spacing or timings.**

### Color palette
```css
:root {
  /* Dark mode (default) */
  --color-bg: #06080c;
  --color-bg-elevated: #0c1016;
  --color-bg-subtle: #10161e;
  --color-bg-glass: rgba(12, 16, 22, 0.85);
  --color-bg-glass-strong: rgba(12, 16, 22, 0.95);
  --color-border: #1a2230;
  --color-border-strong: #243044;
  --color-border-glass: rgba(255, 255, 255, 0.05);
  --color-border-glass-strong: rgba(255, 255, 255, 0.1);

  --color-text: #f5f7fa;
  --color-text-muted: #94a0b2;
  --color-text-faint: #5d6b7f;

  --color-brand: #00e5ff;        /* Electric cyan — main accent */
  --color-brand-dim: #00b8cc;
  --color-brand-hover: #33ebff;
  --color-brand-light: rgba(0, 229, 255, 0.08);
  --color-brand-glow: rgba(0, 229, 255, 0.25);

  --color-success: #10e07a;
  --color-success-light: rgba(16, 224, 122, 0.1);
  --color-warning: #ffd600;
  --color-warning-light: rgba(255, 214, 0, 0.1);
  --color-danger: #ff4757;
  --color-danger-light: rgba(255, 71, 87, 0.1);
}
```

### Light mode override
```css
@media (prefers-color-scheme: light) {
  :root {
    --color-bg: #f2f2f7;
    --color-bg-elevated: #ffffff;
    --color-bg-subtle: #eaeaef;
    --color-bg-glass: rgba(255, 255, 255, 0.9);
    --color-bg-glass-strong: rgba(255, 255, 255, 0.95);
    --color-border: #d1d1d6;
    --color-border-strong: #c6c6cc;
    --color-border-glass: rgba(0, 0, 0, 0.05);
    --color-border-glass-strong: rgba(0, 0, 0, 0.08);
    --color-text: #1d1d1f;
    --color-text-muted: #6e6e73;
    --color-text-faint: #9e9ea3;
    --color-brand: #0066cc;
    --color-brand-dim: #0052a3;
    --color-brand-hover: #0071e3;
    --color-brand-light: rgba(0, 102, 204, 0.08);
    --color-brand-glow: rgba(0, 102, 204, 0.15);
    /* shadows get lighter accordingly */
  }
}
```

### Typography
```css
:root {
  --font-display: -apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Segoe UI Variable', system-ui, sans-serif;
  --font-body: -apple-system, BlinkMacSystemFont, 'SF Pro Text', 'Segoe UI Variable', system-ui, sans-serif;
  --font-mono: 'SF Mono', 'JetBrains Mono', 'Fira Code', monospace;

  /* Fluid clamp scale — no breakpoints needed */
  --text-xs: clamp(0.625rem, 0.6rem + 0.125vw, 0.6875rem);
  --text-sm: clamp(0.75rem, 0.72rem + 0.15vw, 0.8125rem);
  --text-base: clamp(0.875rem, 0.84rem + 0.175vw, 0.9375rem);
  --text-lg: clamp(1rem, 0.95rem + 0.25vw, 1.125rem);
  --text-xl: clamp(1.125rem, 1.05rem + 0.375vw, 1.375rem);
  --text-2xl: clamp(1.375rem, 1.25rem + 0.625vw, 1.75rem);
  --text-3xl: clamp(1.75rem, 1.5rem + 1.25vw, 2.5rem);
  --text-4xl: clamp(2.25rem, 1.875rem + 1.875vw, 3.5rem);
}
```

### Spacing and radii
```css
:root {
  --space-1: 0.25rem;  --space-2: 0.5rem;  --space-3: 0.75rem;
  --space-4: 1rem;     --space-5: 1.25rem; --space-6: 1.5rem;
  --space-7: 1.75rem;  --space-8: 2rem;    --space-10: 2.5rem;
  --space-12: 3rem;    --space-16: 4rem;

  --radius-sm: 8px;    --radius-md: 12px;  --radius-lg: 16px;
  --radius-xl: 20px;   --radius-2xl: 24px; --radius-full: 9999px;
}
```

### Layered shadows
```css
:root {
  --shadow-xs: 0 1px 2px rgba(0,0,0,0.2), 0 1px 1px rgba(0,0,0,0.12);
  --shadow-sm: 0 2px 4px rgba(0,0,0,0.24), 0 1px 2px rgba(0,0,0,0.16);
  --shadow-md: 0 6px 16px -2px rgba(0,0,0,0.3), 0 3px 8px -2px rgba(0,0,0,0.2);
  --shadow-lg: 0 24px 48px -8px rgba(0,0,0,0.4), 0 12px 24px -4px rgba(0,0,0,0.24);
  --shadow-xl: 0 40px 80px -12px rgba(0,0,0,0.48), 0 16px 32px -6px rgba(0,0,0,0.28);
  --shadow-glass: 0 8px 32px rgba(0,0,0,0.36);
  --shadow-glow-brand: 0 0 0 1px rgba(0,229,255,0.15), 0 0 24px rgba(0,229,255,0.12);
}
```

### Spring physics
```css
:root {
  --spring-calm: cubic-bezier(0.32, 0.72, 0, 1);      /* damping 1.0 */
  --spring-snappy: cubic-bezier(0.2, 0.8, 0.2, 1);    /* damping 1.0, faster */
  --spring-bounce: cubic-bezier(0.16, 0.84, 0.44, 1); /* damping 0.8 */
  --spring-expo: cubic-bezier(0.16, 1, 0.3, 1);       /* momentum */

  --transition-instant: 60ms var(--spring-snappy);
  --transition-fast: 120ms var(--spring-snappy);
  --transition-base: 200ms var(--spring-calm);
  --transition-smooth: 300ms var(--spring-calm);
  --transition-slow: 450ms var(--spring-calm);
}
```

### Layout constants
```css
:root {
  --container-max: 1200px;
  --header-height: 72px;
  --header-height-compact: 60px;
}
```

---

## 2. Page skeleton

### Minimal `base.html` (Jinja2)
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{% block title %}Project name{% endblock %}</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=DM+Sans:opsz,wght@9..40,400;9..40,500;9..40,600;9..40,700&family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600;9..144,700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
  {% block extra_head %}{% endblock %}
</head>
<body>
  <header class="site-header">
    <div class="header-inner">
      <h1 class="site-title">Project name <small>Subtitle</small></h1>
      <div class="header-meta">
        <!-- live clock, status pills, avatar, etc. -->
      </div>
    </div>
  </header>

  <main class="container">
    {% block content %}{% endblock %}
  </main>

  {% block extra_scripts %}
    <script src="{{ url_for('static', filename='main.js') }}"></script>
  {% endblock %}
</body>
</html>
```

### Base reset (top of `styles.css`)
```css
*, *::before, *::after { box-sizing: border-box; }

html {
  font-size: 16px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
}

@media (prefers-color-scheme: dark) { html { color-scheme: dark; } }
@media (prefers-color-scheme: light) { html { color-scheme: light; } }

body {
  margin: 0;
  font-family: var(--font-body);
  font-size: var(--text-base);
  line-height: 1.55;
  color: var(--color-text);
  background: var(--color-bg);
  min-height: 100vh;
  background-image:
    radial-gradient(ellipse 60% 40% at 50% -10%, rgba(0, 229, 255, 0.025), transparent),
    radial-gradient(ellipse 40% 60% at 100% 100%, rgba(199, 146, 254, 0.015), transparent);
}

::selection { background: var(--color-brand-light); color: var(--color-brand); }

/* Reduced motion — required */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 3. Core components

### 3.1 Header — glass bar
```css
.site-header {
  position: sticky; top: 0; z-index: 100;
  background: var(--color-bg-glass);
  backdrop-filter: blur(40px) saturate(200%);
  -webkit-backdrop-filter: blur(40px) saturate(200%);
  border-bottom: 1px solid var(--color-border-glass);
  padding: var(--space-3) 0;
  margin: calc(var(--space-6) * -1) calc(var(--space-4) * -1) var(--space-6);
  padding-left: var(--space-4); padding-right: var(--space-4);
  transition: background var(--transition-smooth), border-color var(--transition-smooth), box-shadow var(--transition-smooth);
}
.site-header:hover, .site-header:focus-within {
  border-color: var(--color-border-glass-strong);
  box-shadow: var(--shadow-glass);
}
.header-inner {
  max-width: var(--container-max); margin: 0 auto;
  display: flex; align-items: center; justify-content: space-between;
  gap: var(--space-4); flex-wrap: wrap;
}
.site-title {
  font-family: var(--font-display); font-size: var(--text-2xl); font-weight: 600;
  letter-spacing: -0.03em; color: var(--color-text); margin: 0;
  display: flex; align-items: baseline; gap: var(--space-3);
  background: linear-gradient(135deg, var(--color-text) 0%, var(--color-text-muted) 100%);
  -webkit-background-clip: text; background-clip: text; -webkit-text-fill-color: transparent;
}
.site-title small {
  font-family: var(--font-body); font-size: var(--text-sm); font-weight: 500;
  color: var(--color-text-muted); text-transform: uppercase; letter-spacing: 0.12em;
  background: none; -webkit-text-fill-color: var(--color-text-muted);
}
.live-time {
  font-family: var(--font-mono); font-size: var(--text-lg); font-variant-numeric: tabular-nums;
  font-weight: 500; color: var(--color-text-muted);
  background: var(--color-bg-glass-strong); backdrop-filter: blur(20px);
  border: 1px solid var(--color-border-glass); padding: var(--space-2) var(--space-5);
  border-radius: var(--radius-full); min-width: 92px; text-align: center;
  transition: color var(--transition-fast), border-color var(--transition-fast),
              background var(--transition-fast), box-shadow var(--transition-fast);
}
.live-time.is-soon {
  color: var(--color-brand); border-color: var(--color-brand);
  background: var(--color-brand-light); box-shadow: var(--shadow-glow-brand);
}
.live-time.is-late {
  color: var(--color-danger); border-color: var(--color-danger);
  background: var(--color-danger-light);
  box-shadow: 0 0 0 1px rgba(255,71,87,0.15), 0 0 24px rgba(255,71,87,0.1);
}
```

### 3.2 Container
```css
.container {
  max-width: var(--container-max); margin: 0 auto;
  padding: var(--space-6) var(--space-4);
}
```

### 3.3 Cards — real glassmorphism
```css
.card {
  background: var(--color-bg-glass);
  backdrop-filter: blur(40px) saturate(180%);
  -webkit-backdrop-filter: blur(40px) saturate(180%);
  border: 1px solid var(--color-border-glass);
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-xs), inset 0 1px 0 rgba(255,255,255,0.03);
  overflow: hidden;
  transition: border-color var(--transition-smooth), box-shadow var(--transition-smooth),
              background var(--transition-smooth), transform var(--transition-base);
}
.card:hover {
  border-color: var(--color-border-glass-strong);
  box-shadow: var(--shadow-md), inset 0 1px 0 rgba(255,255,255,0.05);
  transform: translateY(-2px);
}
.card-header {
  display: flex; align-items: center; justify-content: space-between;
  padding: var(--space-4) var(--space-6);
  border-bottom: 1px solid var(--color-border-glass);
  background: linear-gradient(180deg, rgba(255,255,255,0.04), transparent 60%);
}
.card-header h2 {
  margin: 0; font-family: var(--font-display); font-size: var(--text-lg);
  font-weight: 600; letter-spacing: -0.02em;
}
.card-count {
  font-family: var(--font-mono); font-size: var(--text-sm); font-variant-numeric: tabular-nums;
  font-weight: 500; color: var(--color-text-muted);
  background: var(--color-bg-elevated); border: 1px solid var(--color-border);
  padding: var(--space-1) var(--space-4); border-radius: var(--radius-full);
  transition: border-color var(--transition-fast), color var(--transition-fast), background var(--transition-fast);
}
.card-count:hover { border-color: var(--color-brand); color: var(--color-brand); background: var(--color-brand-light); }
.card-body { padding: var(--space-6); }
```

### 3.4 Grid
```css
.grid { display: grid; gap: var(--space-5); }
@media (min-width: 768px) { .grid-2 { grid-template-columns: 1fr 1fr; } }
@media (min-width: 960px) { .grid-3 { grid-template-columns: repeat(3, 1fr); } }
```

### 3.5 Buttons — spring physics and glass variants
```css
.btn {
  display: inline-flex; align-items: center; justify-content: center; gap: var(--space-2);
  padding: var(--space-2) var(--space-5); font-family: var(--font-body);
  font-size: var(--text-sm); font-weight: 500; line-height: 1;
  border: none; border-radius: var(--radius-full); cursor: pointer;
  transition: transform var(--transition-instant), box-shadow var(--transition-fast),
              background var(--transition-fast), border-color var(--transition-fast), color var(--transition-fast);
  text-decoration: none; white-space: nowrap; will-change: transform, box-shadow;
  position: relative; overflow: hidden;
}
.btn::before {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(180deg, rgba(255,255,255,0.15), transparent 50%);
  opacity: 0; transition: opacity var(--transition-fast);
}
.btn:hover::before { opacity: 1; }
.btn:active { transform: scale(0.96); }
.btn:focus-visible { outline: 2px solid var(--color-brand); outline-offset: 3px; }

.btn-primary {
  background: linear-gradient(135deg, var(--color-brand) 0%, var(--color-brand-dim) 100%);
  color: #000;
  box-shadow: 0 2px 8px rgba(0,229,255,0.2), 0 0 0 1px rgba(0,229,255,0.1);
}
.btn-primary:hover {
  box-shadow: 0 4px 16px rgba(0,229,255,0.3), 0 0 0 1px rgba(0,229,255,0.2), 0 0 32px rgba(0,229,255,0.15);
  transform: translateY(-2px);
}
.btn-secondary {
  background: var(--color-bg-glass); backdrop-filter: blur(20px);
  color: var(--color-text); border: 1px solid var(--color-border-glass);
}
.btn-secondary:hover {
  background: var(--color-bg-glass-strong); border-color: var(--color-border-glass-strong);
  transform: translateY(-2px); box-shadow: var(--shadow-md);
}
.btn-ghost { background: transparent; color: var(--color-text-muted); }
.btn-ghost:hover { color: var(--color-text); background: var(--color-bg-subtle); }
.btn svg { width: 16px; height: 16px; flex-shrink: 0; stroke-width: 2.5; transition: stroke var(--transition-fast), transform var(--transition-fast); }
.btn:hover svg { transform: translateX(1px); }
.btn-sm { padding: var(--space-1) var(--space-3); font-size: var(--text-xs); }
```

### 3.6 Status badges
```css
.status-badge,
.status-pill {
  display: inline-flex; align-items: center; padding: var(--space-1) var(--space-3);
  font-size: var(--text-xs); font-weight: 600; text-transform: uppercase;
  letter-spacing: 0.08em; border-radius: var(--radius-full); border: 1px solid currentColor;
}
.status-badge--info { background: var(--color-brand-light); color: var(--color-brand); border-color: var(--color-brand); }
.status-badge--danger { background: var(--color-danger-light); color: var(--color-danger); border-color: var(--color-danger); }
.status-badge--success { background: var(--color-success-light); color: var(--color-success); border-color: var(--color-success); }
.status-pill--done { color: var(--color-success); border-color: var(--color-success); }
.status-pill--todo { color: var(--color-warning); border-color: var(--color-warning); }
.status-pill--progress { color: var(--color-brand); border-color: var(--color-brand); }
```

### 3.7 Status dots
```css
.status-dot {
  width: 8px; height: 8px; border-radius: var(--radius-full);
  background: var(--color-success);
  box-shadow: 0 0 8px var(--color-success);
  animation: pulse 2s ease-in-out infinite;
}
@keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.4; } }
```

---

## 4. Complex patterns

### 4.1 List items with hover shift and accent bar
```css
.list-item {
  display: grid; grid-template-columns: 60px 1fr auto; gap: var(--space-5);
  align-items: start; padding: var(--space-5) var(--space-6);
  background: linear-gradient(135deg, var(--color-bg-glass) 0%, var(--color-bg-subtle) 100%);
  backdrop-filter: blur(20px); border: 1px solid var(--color-border-glass);
  border-radius: var(--radius-lg); will-change: transform, box-shadow, border-color;
  transition: border-color var(--transition-base), box-shadow var(--transition-base),
              transform var(--transition-fast), background var(--transition-base);
  position: relative;
}
.list-item::before {
  content: ''; position: absolute; left: 0; top: 0; bottom: 0; width: 3px;
  background: var(--color-brand); border-radius: var(--radius-lg) 0 0 var(--radius-lg);
  opacity: 0; transform: scaleY(0); transform-origin: top;
  transition: opacity var(--transition-fast), transform var(--transition-base);
}
.list-item:hover {
  border-color: var(--color-brand); transform: translateX(6px);
  box-shadow: var(--shadow-md), inset 0 1px 0 rgba(255,255,255,0.05);
}
.list-item:hover::before { opacity: 1; transform: scaleY(1); }
.list-badge {
  display: flex; align-items: center; justify-content: center;
  width: 48px; height: 48px; border-radius: var(--radius-md);
  font-family: var(--font-display); font-size: var(--text-xl); font-weight: 700;
  color: #000; background: linear-gradient(135deg, var(--color-brand) 0%, var(--color-brand-dim) 100%);
  flex-shrink: 0; box-shadow: 0 2px 8px rgba(0,229,255,0.35), inset 0 1px 0 rgba(255,255,255,0.3);
}
.list-item.inactive { opacity: 0.5; border-color: var(--color-danger-light); background: linear-gradient(135deg, var(--color-danger-light) 0%, var(--color-bg-subtle) 100%); }
.list-item.inactive .list-badge { background: linear-gradient(135deg, var(--color-danger) 0%, #c00 100%); }
```

### 4.2 Schedule grid (columns with rows)
```css
.schedule-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: var(--space-4); }
@media (max-width: 1100px) { .schedule-grid { grid-template-columns: repeat(2, 1fr); } }
@media (max-width: 700px) { .schedule-grid { grid-template-columns: 1fr; } }
.schedule-column {
  background: var(--color-bg-glass); backdrop-filter: blur(40px) saturate(180%);
  border: 1px solid var(--color-border-glass); border-radius: var(--radius-lg); overflow: hidden;
  transition: border-color var(--transition-smooth), box-shadow var(--transition-smooth);
}
.schedule-column:hover { border-color: var(--color-border-glass-strong); box-shadow: var(--shadow-md); }
.schedule-row {
  display: grid; grid-template-columns: 72px 1fr; gap: var(--space-5); align-items: center;
  padding: var(--space-4) var(--space-6); border-bottom: 1px solid var(--color-border-glass);
  transition: background var(--transition-fast); width: 100%; box-sizing: border-box;
}
.schedule-row.highlighted { border-left: 3px solid var(--color-brand); background: var(--color-brand-light); }
.schedule-row.past { opacity: 0.3; background: rgba(0,0,0,0.2); }
.row-label {
  display: flex; flex-direction: column; align-items: flex-end; gap: var(--space-1);
  font-family: var(--font-mono); font-size: var(--text-sm); font-weight: 500;
  font-variant-numeric: tabular-nums; color: var(--color-text-muted); text-align: right;
  padding-right: var(--space-4); border-right: 1px solid var(--color-border-glass);
}
.row-sub { font-size: var(--text-xs); color: var(--color-text-faint); font-weight: 400; }
```

### 4.3 Collapsible groups
Behavior:
- `.group-item.expanded .group-list` → `display: flex` plus the `slideDown` animation
- `.group-entry.editing` → hides the content and shows the form
- `.group-entry:hover .entry-actions` → `opacity: 1`

---

## 5. Entrance choreography

```css
@keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes slideInRight { from { opacity: 0; transform: translateX(-20px); } to { opacity: 1; transform: translateX(0); } }
@keyframes slideDown { from { opacity: 0; transform: translateY(-8px); } to { opacity: 1; transform: translateY(0); } }

.card, .schedule-column { animation: fadeInUp 0.6s var(--spring-calm) backwards; }
.card:nth-child(1) { animation-delay: 0ms; }
.card:nth-child(2) { animation-delay: 50ms; }
.card:nth-child(3) { animation-delay: 100ms; }
.card:nth-child(4) { animation-delay: 150ms; }
.list-item, .group-entry { animation: slideInRight 0.5s var(--spring-calm) backwards; }
.list-item:nth-child(1) { animation-delay: 0ms; }
.list-item:nth-child(2) { animation-delay: 40ms; }
/* continue the pattern for more items */
```

---

## 6. JavaScript (vanilla, no framework)

### 6.1 Module wrapper
```js
(function() {
  'use strict';
  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', init);
  } else { init(); }
  function init() {
    setupFeatureA();
    setupFeatureB();
  }
})();
```

### 6.2 Event delegation (preferred)
```js
document.addEventListener('click', (e) => {
  const target = e.target.closest('[data-action]');
  if (!target) return;
  const action = target.dataset.action;
  if (action === 'cycle-status') cycleStatus(target);
  if (action === 'edit') startEditing(target);
  if (action === 'delete') deleteItem(target);
});
```

### 6.3 Status cycling (optimistic UI + server sync)
```js
const STATUS_CYCLE = ['todo', 'in progress', 'done'];

async function cycleStatus(el) {
  const item = el.closest('[data-id]');
  const id = item.dataset.id;
  const current = item.dataset.status;
  const next = STATUS_CYCLE[(STATUS_CYCLE.indexOf(current) + 1) % STATUS_CYCLE.length];

  item.dataset.status = next;   // optimistic
  renderStatus(item, next);

  try {
    await fetch(`/api/items/${id}`, {
      method: 'PATCH', headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ status: next })
    });
  } catch { rollback(item, current); showToast('Sync failed', 'error'); }
}
```

### 6.4 Inline editing
```js
function startEditing(item) {
  cancelAllEditing();
  item.classList.add('editing');
  item.querySelector('input').focus();
}
function saveEdit(item, form) {
  const data = Object.fromEntries(new FormData(form));
  // validate, PATCH the API, then re-render
  item.classList.remove('editing');
  renderItem(item, data);
}
function cancelAllEditing() {
  document.querySelectorAll('.editing').forEach(el => el.classList.remove('editing'));
}
```

### 6.5 localStorage hydration (server → client)
```js
function initStorageFromDOM() {
  if (localStorage.getItem('data')) return;   // user data already present
  const data = {};
  document.querySelectorAll('[data-id]').forEach(el => {
    data[el.dataset.id] = { /* read from the DOM */ };
  });
  if (Object.keys(data).length) localStorage.setItem('data', JSON.stringify(data));
}
```

### 6.6 Toasts
```js
function showToast(message, type = 'success') {
  const container = document.getElementById('toastContainer') || createToastContainer();
  const toast = document.createElement('div');
  toast.className = `toast ${type}`;
  toast.innerHTML = `<svg class="toast-icon">...</svg><span>${escapeHtml(message)}</span>`;
  container.appendChild(toast);
  setTimeout(() => {
    toast.style.animation = 'slideInRight 0.3s var(--spring-snappy) reverse';
    setTimeout(() => toast.remove(), 300);
  }, 3000);
}
```
Note: `escapeHtml` is required whenever user text ends up in `innerHTML`.

---

## 7. Accessibility (WCAG 2.2 AA)

- [ ] Semantic HTML: `<header>`, `<main>`, `<section>`, `<article>`, `<nav>`, `<footer>`
- [ ] Headings: exactly one `<h1>`, then `<h2>`/`<h3>` in logical order
- [ ] Visible focus: `:focus-visible { outline: 2px solid var(--color-brand); outline-offset: 3px; }`
- [ ] Contrast: text at least 4.5:1 (large text 3:1); verify when you change token values
- [ ] `aria-label` on icon-only buttons
- [ ] Live regions for dynamic updates: `<div aria-live="polite" id="toastContainer">`
- [ ] Reduced motion respected (see base reset)
- [ ] Keyboard operable: every element reachable, Enter/Space activate
- [ ] Form fields have `<label for>` or `aria-label`/`aria-labelledby`
- [ ] `lang` attribute on `<html>` and on sections in another language

---

## 8. Performance

| Rule | How |
|-------|-----------|
| Font-Preconnect | `<link rel="preconnect" href="https://fonts.googleapis.com">` |
| CSS in `<head>` | One `styles.css`, no `@import` |
| JS at the end | `defer` or a module script before `</body>` |
| No layout shift | Reserve space for the live clock and toasts, `aspect-ratio` on media |
| Lean painting | `will-change` only on animated elements |
| Compression | Brotli/gzip on the server, `Cache-Control: immutable` for versioned assets |

---

## 9. Don'ts

- No hard-coded hex colors, pixel values or `cubic-bezier()` in components
- No `transition: all`; list the properties explicitly
- Never drop reduced motion support
- No font families beyond display, body and mono
- `box-shadow` only through the shadow tokens
- Don't nest more than two levels of cards
- Use the pixel radius tokens for `border-radius`, not `rem`, to keep edges crisp

---

## 10. Build workflow

1. Copy the tokens, base reset and components from this skill into `styles.css`.
2. Create `base.html` with header, container and blocks.
3. Page templates extend `base.html`.
4. Vanilla JS in IIFE modules, events via delegation.
5. Test light/dark mode, reduced motion and keyboard use.
6. Check contrast in the browser dev tools.
7. Add entrance animations with staggered delays.

---

## 11. Related skills

If installed, these pair well: `frontend-design` (your own visual direction), `motion-foundations` (spring tokens, reduced motion), `frontend-a11y` (accessibility), `make-interfaces-feel-better` (polish for spacing, shadows and motion).

