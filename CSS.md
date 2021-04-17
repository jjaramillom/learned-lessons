# CSS

## Problem

Which CSS naming convention(Architecture) to use.

## Solution

There are a bunch of options, being the most famous BEM, OOCSS, and Atomic. Since I use mostly React and (S)CSS modules, I went for a modified BEM based on this [article](https://medium.com/trabe/a-comprehensive-guide-to-using-bem-with-react-14d00c199e0d).

The main idea is to make CSS classes/selectors friendlier to use within React components.

It goes the following way.

1. Everything are written using _camelCase_. eg. `table`
2. Elements are written using _camelCase_, and are joined to the block name using a single underscore `_`. eg. `table_header`
3. Modifiers are written using _camelCase_ and are joined to the block/element name using three underscores `___`. eg. `table_header___highlighted`

Some examples...

### HTML

```html
<div class="component">
  <div class="component____childElement"></div>
</div>
<div class="component component_reversed">
  <div class="component___childElement"></div>
</div>
```

### CSS

```scss
.component {
  $self: &;
  // ...

  &___childElement {
    // ...
  }

  &_reversed {
    // ...

    #{ $self }___childElement {
      // ...
    }
  }
}
```
