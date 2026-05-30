# Skill: Accessibility (A11Y)

## Description
Implements web accessibility following WCAG 2.1 guidelines. Ensures interfaces are usable by everyone including people with disabilities.

## When to Use
- Building new interfaces
- Audit existing sites
- Fixing accessibility issues
- Compliance requirements

## Instructions

### WCAG 2.1 Levels
| Level | Description |
|-------|-------------|
| A | Minimum accessibility |
| AA | Standard (target) |
| AAA | Highest (optional) |

### Semantic HTML
```html
<!-- Good -->
<header>
  <nav aria-label="Main">
    <ul>
      <li><a href="/home">Home</a></li>
    </ul>
  </nav>
</header>

<main>
  <article>
    <h1>Page Title</h1>
    <section aria-labelledby="section-title">
      <h2 id="section-title">Section</h2>
    </section>
  </article>
</main>

<footer>
  <p>© 2026</p>
</footer>

<!-- Bad -->
<div class="header">
  <div class="nav">...</div>
</div>
<div class="main">
  <div class="content">...</div>
</div>
```

### ARIA Labels
```html
<!-- Buttons -->
<button aria-label="Close menu">×</button>
<button aria-describedby="tooltip-1">Info</button>

<!-- Navigation -->
<nav aria-label="Primary">...</nav>
<nav aria-label="Footer">...</nav>

<!-- Forms -->
<label for="email">Email</label>
<input id="email" aria-required="true" aria-invalid="false">

<!-- Live regions -->
<div aria-live="polite" aria-atomic="true">
  {statusMessage}
</div>
```

### Keyboard Navigation
```typescript
// Handle keyboard events
const handleKeyDown = (e: React.KeyboardEvent) => {
  if (e.key === 'Enter' || e.key === ' ') {
    handleClick();
  }
  if (e.key === 'Escape') {
    closeModal();
  }
};

// Focus management
const modalRef = useRef<HTMLDivElement>(null);

useEffect(() => {
  modalRef.current?.focus();
}, []);
```

### Color Contrast
```
Normal text: 4.5:1 minimum
Large text: 3:1 minimum
UI components: 3:1 minimum

Tools:
- Chrome DevTools > Accessibility
- axe DevTools extension
- WAVE extension
```

### Images and Media
```html
<!-- Informative image -->
<img src="chart.png" alt="Sales increased 20% in Q4">

<!-- Decorative image -->
<img src="decoration.svg" alt="">

<!-- Complex image -->
<figure>
  <img src="chart.png" alt="..." aria-describedby="chart-desc">
  <figcaption id="chart-desc">
    Detailed description of the chart...
  </figcaption>
</figure>
```

### Testing Accessibility
```bash
# axe-core
npm install --save-dev axe-core @axe-core/react

# Lighthouse
npm install --save-dev lighthouse

# Manual testing checklist
- [ ] Tab through all interactive elements
- [ ] Screen reader test (NVDA/VoiceOver)
- [ ] Color contrast check
- [ ] Keyboard-only navigation
- [ ] Focus visible indicators
```

### Quick Checklist
- [ ] All images have alt text
- [ ] Form inputs have labels
- [ ] Heading hierarchy is logical (h1 > h2 > h3)
- [ ] Color is not the only way to convey information
- [ ] Interactive elements are keyboard accessible
- [ ] Focus indicators are visible
- [ ] ARIA labels are used correctly
- [ ] Page has proper lang attribute

## References
- [[HTML5 - Referência Completa]]
- [[CSS3 - Referência Completa]]
