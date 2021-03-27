# Some cool tips from Platzi-day.

### 1. Better `index` files

replace

```typescript
import Something from './Something';
import SomethingElse from './SomethingElse';

export { Something, SomethingElse };
```

for

```typescript
export { default as Something } from './Something';
export { default as SomethingElse } from './SomethingElse';
```
