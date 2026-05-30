# Skill: API Integration

## Description
Consumes and creates REST and GraphQL APIs with proper error handling, caching, and best practices.

## When to Use
- Consuming third-party APIs
- Creating API endpoints
- Integrating frontend with backend
- Handling authentication

## Instructions

### REST API Consumption

#### Basic Fetch
```typescript
// GET request
const response = await fetch('https://api.example.com/users');
const data = await response.json();

// POST request
const response = await fetch('https://api.example.com/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({ name: 'John' }),
});

// Error handling
if (!response.ok) {
  throw new Error(`HTTP error! status: ${response.status}`);
}
```

#### Custom Hook
```typescript
function useFetch<T>(url: string) {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    async function fetchData() {
      try {
        const response = await fetch(url);
        if (!response.ok) throw new Error('Failed to fetch');
        const json = await response.json();
        setData(json);
      } catch (err) {
        setError(err instanceof Error ? err.message : 'Unknown error');
      } finally {
        setLoading(false);
      }
    }
    fetchData();
  }, [url]);

  return { data, loading, error };
}

// Usage
const { data, loading, error } = useFetch<User[]>('/api/users');
```

#### Axios Alternative
```typescript
import axios from 'axios';

const api = axios.create({
  baseURL: 'https://api.example.com',
  timeout: 5000,
  headers: { 'Content-Type': 'application/json' },
});

// Request interceptor
api.interceptors.request.use((config) => {
  const token = localStorage.getItem('token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Response interceptor
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      // Handle unauthorized
    }
    return Promise.reject(error);
  }
);
```

### GraphQL

#### Basic Query
```typescript
const query = `
  query GetUsers {
    users {
      id
      name
      email
    }
  }
`;

const response = await fetch('https://api.example.com/graphql', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ query }),
});

const { data } = await response.json();
```

#### With Variables
```typescript
const query = `
  query GetUser($id: ID!) {
    user(id: $id) {
      id
      name
      posts {
        title
      }
    }
  }
`;

const response = await fetch('https://api.example.com/graphql', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    query,
    variables: { id: '123' },
  }),
});
```

### Error Handling Pattern
```typescript
class ApiError extends Error {
  constructor(
    public status: number,
    message: string,
    public data?: unknown
  ) {
    super(message);
  }
}

async function apiRequest<T>(url: string, options?: RequestInit): Promise<T> {
  const response = await fetch(url, {
    ...options,
    headers: {
      'Content-Type': 'application/json',
      ...options?.headers,
    },
  });

  if (!response.ok) {
    const data = await response.json().catch(() => null);
    throw new ApiError(response.status, response.statusText, data);
  }

  return response.json();
}

// Usage
try {
  const users = await apiRequest<User[]>('/api/users');
} catch (error) {
  if (error instanceof ApiError) {
    console.error(`API Error ${error.status}: ${error.message}`);
  }
}
```

### Caching Strategies
```typescript
// Simple in-memory cache
const cache = new Map<string, { data: unknown; expiry: number }>();

async function fetchWithCache<T>(url: string, ttl = 60000): Promise<T> {
  const cached = cache.get(url);
  if (cached && cached.expiry > Date.now()) {
    return cached.data as T;
  }

  const data = await apiRequest<T>(url);
  cache.set(url, { data, expiry: Date.now() + ttl });
  return data;
}
```

### API URLs for Practice
| API | URL | Use Case |
|-----|-----|----------|
| JSONPlaceholder | jsonplaceholder.typicode.com | CRUD mock |
| PokéAPI | pokeapi.co | Fun data |
| Rick and Morty | rickandmortyapi.com | Characters |
| GitHub | api.github.com | Real data |
| OpenWeather | openweathermap.org | Weather app |

## References
- [[APIs REST e GraphQL]]
- [[JavaScript - Referência Completa]]
- [[React - Referência Completa]]
