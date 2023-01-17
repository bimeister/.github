# CSS Style Guide

#### 1. Deprecated or production unready syntax is not allowed.

> Deprecated syntax is not recommended for use for various reasons - it may be slow in performance, it may only be supported by some browsers or outdated. In any case, we must choose reliable and efficient methods for solving problems.

```css
/* 👎 Inalid usage: */
* {
  overflow: overlay;
}

/* 👍 Valid usage: */
* {
  overflow: hidden;
  /* ... custom scrollbar */
}
```

#### 2. SCSS-variables for property values should be named according to the pattern: `$applied-property_pointer-to-context`.

> This convention of naming variables allows you to increase their readability due to the fact that the name immediately reflects the context in which the value is used.

```scss
/* 👎 Inalid usage: */
$width: 100%;
$plf: 1rem;

/* 👍 Valid usage: */
$width_header: 100%;
$padding-left_footer: 1rem;
```
