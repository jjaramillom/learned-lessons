# TypeScript

**Problem** => When there's a type such as

```typescript
type Route 'main' | 'detail'
type RouteConfig: {}
type Routes{
  [key:Route]: RouteConfig
}
const routes:Routes = {}
```

TypeScript provides a Type `Record<K,T>` which is quite useful.

```typescript
type Route 'main' | 'detail'
const routes: Record<Route, RouteConfig>
```

**Solution** =>
