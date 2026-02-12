## Preprocessors & Methodologies in CSS  

## 1. Sass Basics (the most popular preprocessor)

### 1.1 What is Sass?

Sass (usually written in SCSS syntax) is **not understood by browsers directly**.

You write Sass → a compiler converts it into normal CSS → browser uses CSS.

Sass adds features that plain CSS didn’t originally have (many are still unique):

- Variables
- Nesting
- Mixins
- Functions
- File splitting (partials)

Example (Sass):

    $primary: #1f8ef1;

    button {
      background-color: $primary;
    }

Compiled CSS output:

    button {
      background-color: #1f8ef1;
    }

Important rule:
You never ship `.scss` files to users — only compiled `.css`.

---

### 1.2 Sass Variables vs CSS Variables

Sass variables use `$`:

    $primary: #1f8ef1;
    $spacing-md: 1rem;
    $radius-md: 0.75rem;

Use them:

    button {
      background: $primary;
      padding: $spacing-md;
      border-radius: $radius-md;
    }

Key difference from CSS variables:

- Sass variables are **compile-time**
- CSS variables are **runtime**

Meaning:

- Sass variables disappear after compilation
- CSS variables can change dynamically (themes, dark mode)

You can combine both:

    :root {
      --primary: #{$primary};
    }

Sass injects its value into a CSS variable.

---

### 1.3 Nesting (write CSS like HTML)

Plain CSS:

    .card { }
    .card h3 { }
    .card p { }

Sass nesting:

    .card {
      padding: 1rem;
      background: #fff;

      h3 {
        margin-bottom: 0.5rem;
      }

      p {
        color: #555;
      }
    }

Compiled output is the same.

Important warning:
Do NOT over-nest.

Bad:

    .page {
      .container {
        .card {
          .title { }
        }
      }
    }

This creates very specific selectors that are hard to override.

Good rule:
- Nest only 1–2 levels
- Nest elements inside a block, not entire page structures

---

### 1.4 The & (parent selector)

`&` means “the current selector”.

Used for:
- Hover
- Active states
- BEM modifiers

Example:

    .button {
      background: $primary;
      color: white;

      &:hover {
        background: darken($primary, 10%);
      }

      &--secondary {
        background: white;
        color: $primary;
        border: 1px solid $primary;
      }
    }

Compiles to:

    .button { }
    .button:hover { }
    .button--secondary { }

This is extremely powerful with BEM.

---

### 1.5 Mixins (reusable patterns)

Mixins let you reuse chunks of CSS.

Example: flex centering

    @mixin flex-center {
      display: flex;
      align-items: center;
      justify-content: center;
    }

Use it:

    .hero {
      @include flex-center;
      min-height: 60vh;
    }

Mixins with arguments:

    @mixin button-base($bg, $color) {
      background: $bg;
      color: $color;
      padding: 0.5rem 1rem;
      border-radius: 999px;
      border: none;
      cursor: pointer;
    }

    .btn-primary {
      @include button-base($primary, white);
    }

    .btn-secondary {
      @include button-base(white, $primary);
      border: 1px solid $primary;
    }

---

### 1.6 Partials & @use (splitting files)

Large projects must be split into files.

Sass partials start with `_`.

Files:

    _variables.scss
    _mixins.scss
    _buttons.scss

Modern import method: `@use`

Example:

    // _colors.scss
    $primary: #1f8ef1;

    // main.scss
    @use "colors";

    button {
      background: colors.$primary;
    }

This prevents global pollution and keeps things organized.

---

### 1.7 Sass Functions (brief)

Built-in functions:

    darken($primary, 10%)
    lighten($primary, 15%)

Used mostly for color manipulation.

---

## 2. BEM Methodology

### 2.1 Why BEM Exists

Without naming rules, CSS becomes:

    .container .left .big .red { }

Problems:
- Hard to understand
- Easy to break
- Tied to HTML structure

BEM gives **predictable, readable names**.

---

### 2.2 BEM Structure

BEM = Block, Element, Modifier

Naming pattern:

    .block
    .block__element
    .block--modifier
    .block__element--modifier

Meaning:
- Block → standalone component
- Element → part inside block
- Modifier → variation/state

---

### 2.3 BEM Card Example

HTML:

    <article class="card card--featured">
      <img class="card__image">
      <h3 class="card__title">Title</h3>
      <p class="card__text">Text</p>
      <button class="card__button card__button--primary">Read</button>
    </article>

CSS:

    .card {
      background: white;
      border-radius: 0.75rem;
      padding: 1rem;
    }

    .card--featured {
      border: 2px solid #1f8ef1;
    }

    .card__image { }
    .card__title { }
    .card__text { }

    .card__button { }
    .card__button--primary { }

Benefits:
- No dependency on HTML nesting
- Safe reuse anywhere
- Easy to read & maintain

---

### 2.4 BEM + Sass (perfect combo)

    .card {
      padding: 1rem;

      &--featured {
        border: 2px solid $primary;
      }

      &__title {
        margin-bottom: 0.5rem;
      }

      &__button {
        padding: 0.5rem 1rem;

        &--primary {
          background: $primary;
          color: white;
        }
      }
    }

---

## 3. OOCSS & SMACSS (CSS architecture ideas)

### 3.1 OOCSS (Object Oriented CSS)

Idea:
Treat visual patterns as reusable objects.

Principles:
- Separate structure from skin
- Objects should not depend on location

Example:

    .media {
      display: flex;
      gap: 0.75rem;
    }

    .media__image { }
    .media__body { }

    .media--card {
      background: white;
      padding: 1rem;
      border-radius: 0.75rem;
    }

Same structure, different skins.

---

### 3.2 SMACSS (CSS organization system)

SMACSS divides CSS into categories:

Base  
Layout  
Module  
State  
Theme  

Examples:

Base:
    body, h1, p

Layout:
    .l-header
    .l-sidebar

Module:
    .card
    .button

State:
    .is-active
    .is-hidden

Theme:
    .theme-dark

---

### 3.3 SMACSS Folder Structure

    base/
    layout/
    modules/
    state/
    theme/

BEM usually lives inside **modules**.

---

## 4. Component-Based Styling (modern mindset)

Modern UI = components.

Each component has:
- HTML
- CSS
- JS (optional)

---

### 4.1 Component-Based CSS with BEM + Sass

One component = one block + one partial.

    components/_card.scss
    components/_button.scss

Each file styles only its own component.

---

### 4.2 CSS Modules (concept)

CSS file becomes scoped automatically.

    .card { }

Becomes internally:

    .card_3jf92

Used heavily in React / Next.js.

---

### 4.3 CSS-in-JS (concept)

Styles written inside JS files.

Styles are tied directly to components and props.

You don’t need this yet — concept awareness is enough.

---

## 5. How Everything Fits Together

These tools do NOT compete.

They stack:

- Sass → better CSS syntax & tooling
- BEM → predictable naming
- OOCSS / SMACSS → architecture & structure
- Component-based styling → mindset

Real-world stack:

- SCSS files
- SMACSS folder structure
- BEM class names
- Components importing their own styles

---

## 6. Mental Map (memorize this)

Sass:
- $variables
- nesting (1–2 levels)
- @mixin / @include
- partials + @use

BEM:
- block__element--modifier
- predictable & reusable

OOCSS:
- reuse objects
- separate structure & skin

SMACSS:
- base / layout / module / state / theme

Component-based:
- styles grouped by component
- works with or without frameworks
