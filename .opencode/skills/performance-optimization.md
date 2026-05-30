# Skill: Performance Optimization

## Description
Optimizes web application performance including Core Web Vitals, bundle size, loading speed, and runtime performance.

## When to Use
- Site loading slowly
- Poor Lighthouse scores
- Large bundle sizes
- Runtime performance issues

## Instructions

### Core Web Vitals
| Metric | Target | What it Measures |
|--------|--------|------------------|
| LCP | < 2.5s | Largest Contentful Paint |
| FID | < 100ms | First Input Delay |
| CLS | < 0.1 | Cumulative Layout Shift |
| INP | < 200ms | Interaction to Next Paint |

### Quick Wins

#### Images
```html
<!-- Use modern formats -->
<picture>
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="..." loading="lazy">
</picture>

<!-- Specify dimensions to prevent CLS -->
<img src="..." width="800" height="600" alt="...">
```

#### Code Splitting
```typescript
// React lazy loading
const HeavyComponent = React.lazy(() => import('./HeavyComponent'));

// Route-based splitting
const Home = React.lazy(() => import('./pages/Home'));
const About = React.lazy(() => import('./pages/About'));
```

#### Bundle Analysis
```bash
# Analyze bundle size
npx vite-bundle-visualizer

# Or with webpack
npx webpack-bundle-analyzer stats.json
```

### Lighthouse Checklist
- [ ] Performance score > 90
- [ ] No render-blocking resources
- [ ] Properly sized images
- [ ] Minified CSS/JS
- [ ] Efficient cache policy
- [ ] No unused CSS/JS

### React Performance
```typescript
// Memoize expensive calculations
const expensive = useMemo(() => data.map(...), [data]);

// Memoize callbacks
const handleClick = useCallback(() => {
  doSomething(prop);
}, [prop]);

// Avoid unnecessary re-renders
const MemoizedChild = React.memo(({ data }) => {
  return <div>{/* ... */}</div>;
});
```

### CSS Performance
```css
/* Use will-change for animations */
.animated {
  will-change: transform, opacity;
}

/* Avoid layout thrashing */
.bad { margin: 10px; padding: 5px; } /* 2 reflows */
.good { margin: 10px; } /* 1 reflow */
```

## References
- [[CSS3 - Referência Completa]]
- [[React - Referência Completa]]
