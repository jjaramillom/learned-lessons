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

### Emotion => Cool for managing dynamic styling. Allows adding pseudo-classes to inline CSS.

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

## JavaScript

### Lerna => Tool for managing mono-repos.

1. Create a the mono repo folder.

2. Initialize Lerna. `npx lerna init`

3. Create the "sub-repos" under the `packages` folder. The folder structure should look something like:

```
├── packages
│   ├── client
│   ├── server
├── README.md
├── package.json
├── lerna.json
├── .gitignore
└── node_modules
```

4. The idea is to have one main `node_modules`. For this, we execute first `npx lerna clean -y` to clean the "sub-repos" `node_modules`. Then, to install the respective node_modules in the common folder, we execute `npx lerna bootstrap`.

5. If I have the following files: 

`./packages/client/package.json`
```json
{
  "name": "client",
  "scripts": {
    "start": "node index.js",
  }
}
```

`./packages/server/package.json`
```json
{
  "name": "server",
  "scripts": {
    "start": "node index.js",
  }
}
```

I could have in the main `package.json` the following.

`./package.json`
```json
{
  "name": "server",
  "scripts": {
    "start:all": "lerna run start",
    "start:client" : "lerna run start --scope=client",
    "start:server" : "lerna run start --scope=server",
    "start:client-server" : "lerna run start --scope={client,server}"
  }
}
```

With this, I could set which applications should execute a certain script.