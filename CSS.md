# (S)CSS

## (S)CSS modules cool tricks

### 1. Composition

It is possible to "inherit" existing classes using CSS modules.

```scss
.link {
...
}

.button {
...
}

.linkAlternate {
  composes: link;
}

// It's even possible to inherit from two classes.
.linkSecondary {
  composes: link button;
}

// It's also possible to extend from different files.
.linkExternal {
  composes: link from './links.module.scss';
}
```

## 2. Global classes

To include classes that will be taken as global, just add the keyword `:global` as a prefix.

```scss
:global .title {
  font-size: 20px;
}
```

It's also possible to assign it as

```scss
:global {
  .title {
    font-size: 20px;
  }
}
```

Then just add it as `className="title"` to the component.

## 3. Add multiple imports.
