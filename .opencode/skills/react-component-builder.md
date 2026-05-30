# Skill: React Component Builder

## Description
Creates reusable React components following best practices with TypeScript, proper patterns, and documentation.

## When to Use
- Creating new React components
- Refactoring existing components
- Building component libraries
- Implementing design systems

## Instructions

### Component Structure
```typescript
// ComponentName.tsx
import { useState } from 'react';

interface ComponentProps {
  title: string;
  children: React.ReactNode;
}

export function ComponentName({ title, children }: ComponentProps) {
  return (
    <div className="component">
      <h2>{title}</h2>
      {children}
    </div>
  );
}
```

### Best Practices
1. **Use TypeScript** — Always type props
2. **Component name** — PascalCase, descriptive
3. **One component per file** — Clean exports
4. **Props interface** — Define above component
5. **Default export** — At bottom of file

### File Naming
```
components/
├── Button/
│   ├── Button.tsx
│   ├── Button.test.tsx
│   ├── Button.styles.css
│   └── index.ts
├── Card/
│   └── ...
└── index.ts
```

### Hooks Usage
```typescript
// useState for local state
const [isOpen, setIsOpen] = useState(false);

// useEffect for side effects
useEffect(() => {
  fetchData();
}, []);

// useMemo for expensive calculations
const filtered = useMemo(() => items.filter(...), [items]);

// useCallback for memoized functions
const handleClick = useCallback(() => {
  // ...
}, [dependency]);
```

### Testing
```typescript
import { render, screen, fireEvent } from '@testing-library/react';
import { ComponentName } from './ComponentName';

describe('ComponentName', () => {
  it('renders correctly', () => {
    render(<ComponentName title="Test" />);
    expect(screen.getByText('Test')).toBeInTheDocument();
  });
});
```

## References
- [[React - Referência Completa]]
- [[Testes - Jest e Testing Library]]
- [[TypeScript - Referência Completa]]
