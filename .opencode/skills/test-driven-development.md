# Skill: Test Driven Development

## Description
Implements TDD workflow with Jest and React Testing Library. Writes tests before code, ensuring quality and reliability.

## When to Use
- Creating new features with tests first
- Fixing bugs (write test that reproduces, then fix)
- Refactoring code safely
- Ensuring code coverage

## Instructions

### TDD Cycle
```
1. RED   — Write a failing test
2. GREEN — Write minimum code to pass
3. REFACTOR — Improve code while tests pass
```

### Jest Setup
```bash
npm install --save-dev jest @testing-library/react @testing-library/jest-dom
```

### Test Structure
```typescript
// feature.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { Component } from './Component';

describe('Component', () => {
  // Arrange
  beforeEach(() => {
    render(<Component />);
  });

  it('renders correctly', () => {
    // Assert
    expect(screen.getByText('Expected')).toBeInTheDocument();
  });

  it('handles user interaction', () => {
    // Act
    fireEvent.click(screen.getByRole('button'));
    // Assert
    expect(screen.getByText('Result')).toBeInTheDocument();
  });
});
```

### Common Matchers
```typescript
// Existence
expect(el).toBeInTheDocument();
expect(el).not.toBeInTheDocument();

// Text
expect(el).toHaveTextContent('text');
expect(el).toContainHTML('<div>');

// Classes
expect(el).toHaveClass('active');
expect(el).not.toHaveClass('disabled');

// Attributes
expect(el).toHaveAttribute('href', '/path');
expect(el).toHaveValue('input value');

// Styles
expect(el).toHaveStyle({ color: 'red' });
```

### Mocking
```typescript
// Mock function
const mockFn = jest.fn();
expect(mockFn).toHaveBeenCalledTimes(1);
expect(mockFn).toHaveBeenCalledWith('arg');

// Mock module
jest.mock('./module', () => ({
  fetchData: jest.fn(),
}));

// Mock API
global.fetch = jest.fn(() =>
  Promise.resolve({
    json: () => Promise.resolve({ data: 'test' }),
  })
);
```

### React Testing Library Best Practices
1. **Use accessible queries** — `getByRole`, `getByLabelText`
2. **Avoid** — `getByTestId` as last resort
3. **User events** — Use `@testing-library/user-event`
4. **Async** — Use `waitFor` and `findBy*`

## References
- [[Testes - Jest e Testing Library]]
- [[React - Referência Completa]]
