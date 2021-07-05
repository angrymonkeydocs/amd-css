# Angry Monkey Docs CSS Naming Convention

## Main concerns

* Clean HTML.
* Clean LESS/SASS.
* Reduce HTML size since it's not cacheable.
* Prevent cross selector for depended elements.

## Basics

Provide each parent element (block) with a unique class with no separators (- nor _).

```html
.element

<!-- Html -->
<div class="element"></div>
```

Any inside element should be precedded by a dash (-), except content sectioning elements (section, article, aside, h1..h6, header, footer, ...).

```html
.element h1
.element-description
.element-items
.element-item

<!-- Html -->
<div class="element">
    <h1>Title</h1>
    <p class="element-description">Description text.</p>

    <ul class="element-items">
        <li class="element-item">Item 1</li>
        <li class="element-item">Item 2</li>
        <li class="element-item">Item 3</li>
    </ul>
</div>
```

Adjectives should be started with an underscore (_) without being attached to the element, sub-adjectives should be separated by a dash (-)

```html
.elemt-item._active
.elemt-item._primary
.element-description._color-black

<!-- Html -->
<div class="element">
    <h1>Title</h1>
    <p class="element-description _color-black">Description text.</p>

    <ul class="element-items">
        <li class="element-item _active _primary">Item 1</li>
        <li class="element-item">Item 2</li>
        <li class="element-item">Item 3</li>
    </ul>
</div>
```

Full CSS

```LESS
/* CSS */
.element {}

.element h1 {}

.element-description {}

.element-description._color-black {}

.element-items {}

.element-item {}

.element-item._active {}

.element-item._primary {}

/* LESS/SAAS */
.element {
    h1 { }

    &-description{
        &._color {
            &-black {

            }
        }
    }

    &-items {}

    &-item {
        &._active {}

        &._primary {}
    }
}
```

## BEM Sample

```HTML
<!-- HTML -->
<!-- ----------------------- -->

<!-- Using BEM -->

<form class="form form--theme-christmas form--simple">
    <input class="form__input" type="text" />
    <input class="form__submit form__submit--disabled" type="submit" />
</form>

<!-- Using Angry Monkey -->

<form class="form _theme-christmas _simple">
    <input class="form-input" type="text" />
    <input class="form-submit _disabled" type="submit" />
</form>
```

```LESS
/* CSS */
/* ----------------------- */

/* Using BEM */

.form {}
.form--theme-christmas {}
.form--simple {}
.form__input {}
.form__submit {}
.form__submit--disabled {}


/* Using Angry Monkey */

.form {}
.form._theme-christmas {}
.form._simple {}
.form-input {}
.form-submit {}
.form-submit._disabled {}

/* LESS/SAAS */
/* ----------------------- */

/* Using BEM */

.form {
    &--theme {
        &-christmas {}
    }
    &--simple {}

    &__input {}
    &__submit {
        &--disabled {}
    }
}

/* Using Angry Monkey */

.form {
    &._theme {
        &-christmas{}
    }
    &._simple {}

    &-input {}
    &-submit {
        &._disabled{}
    }
}
```

## Never

### Use adjective in CSS without its parent element

---

**Do**

```css
/* CSS */
.element._adjective { }
```

**Don't**

```css
/* CSS */
._adjective { }
```

### Use LESS or SASS and always include body with header and footer as below

---

**Do**

```less
/* CSS */
body > header {}
body > footer {}

/* LESS/SASS */
body {
    > header {}
    > footer {}
}
```

**Don't**

```less
/* CSS/LESS/SASS */
header {}
footer {}
```

## Prevent

### More than 1 sub class naming

---

**Recommended**

```html
<!-- Html -->
<div class="element">
    <ul class="element-items">
        <li class="element-item">Item 1</li>
        <li class="element-item">Item 2</li>
        <li class="element-item">Item 3</li>
    </ul>
</div>
```

**Not Recommended**

```html
<!-- Html -->
<div class="element">
    <ul class="element-items">
        <li class="element-items-item">Item 1</li>
        <li class="element-items-item">Item 2</li>
        <li class="element-items-item">Item 3</li>
    </ul>
</div>
```

### Classes for content sectioning elements within defined elements

---

**Recommended**

```html
<!-- Html -->
<body>
    <header>
        <nav></nav>
    </header>
</body>
```

```less
/* CSS */
body > header nav {}
```

**Not Recommended**

```html
<!-- Html -->
<body>
    <header class="header">
        <nav class="header-nav"></nav>
    </header>
</body>
```

```less
/* CSS */
.header-nav {}
```

**Recommended**

```html
<!-- Html -->
<div class="element">
    <h1></h1>
    <p class="element-description"></p>
</div>
```

**Not Recommended**

```html
<!-- Html -->
<div class="element">
    <h1 class="element-title"></h1>
    <p class="element-description"></p>
</div>
```

## Better

### Use LESS or SASS and always include main as prefix for page specific content

---

**Recommended**

```less
/* LESS/SASS */
main {
    .element {}
    .form {}
}
```

**Not Recommended**

```less
/* CSS/LESS/SASS */
.element {}
.form {}
```
