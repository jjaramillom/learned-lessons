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

## 3. `@import` shouldn't be used.

The use of `@import` has been deprecated for a while now. Nevertheless a lot of people still use it. Instead of using it, use `@use`.

Before it was:

```scss
@import 'abstracts/variables';
.something {
  color: $red;
}
```

The only difference is that the imports become "namespaced", so to access them, we should add the file prefix. This is to prevent collisions.

It is also possible to add a custom name to the namespace as

```scss
@use 'abstracts/variables' as v;
.something {
  color: v.$red;
}
```

or even take it away with

```scss
@use 'abstracts/variables' as *;
.something {
  color: $red;
}
```

## 4. Usage of `@forward`

It happens sometimes that there are a bunch of files being imported in a SCSS module. E.g.

```scss
@use 'abstracts/variables';
@use 'abstracts/colors';
@use 'abstracts/mixins';
@use 'abstracts/functions';

.something {
  color: colors.$red;
}
//...
```

For this, there is a solution quite similar to JS index files.

We create a `_index.scss` file in the **abstracts** folder such as:

```scss
@forward 'abstracts/variables';
@forward 'abstracts/colors';
@forward 'abstracts/mixins';
@forward 'abstracts/functions';
```

Then, in the module we just use this as:

```scss
@use 'abstracts';

.something {
  color: abstracts.$red;
}
//...
```
