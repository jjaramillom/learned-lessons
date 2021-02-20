# Tools

## Cross-platform

1. Micro. Command line text editor.
1. Nano. Command line text editor.

## Windows

1. Keypirinha. Cool launcher.
2. Everything. Fast searcher
3. Ditto. Clipboard manager.

## Linux

<br/>

# Libraries

## React

1. Emotion => Cool for managing dynamic styling. Allows adding pseudo-classes to inline CSS.

In order to use it with typescript, the following must be done.

```typescript
/** @jsxRuntime classic */
/** @jsx jsx */
import { jsx, css } from '@emotion/react';
...
const Component = ({bgColor, bgHoverColor }) => {
  const style = css`
    background-color: ${bgColor};
    &:hover {
      background-color: ${hoverColor};
    }
  `;
  return <div style={style}></div>;
};
```
