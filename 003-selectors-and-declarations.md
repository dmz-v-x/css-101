## Selectors and Declarations

### 1. The very basic shape of CSS

Before learning selectors, specificity, or media queries, you must clearly understand **what a CSS rule looks like**.

A CSS rule (also called a rule-set) has this shape:

    selector {
      property: value;
      property2: value2;
    }

This structure **never changes**, no matter how advanced CSS becomes.

---

### 2. Selector — the “who” part

The **selector** answers one question:

Which HTML elements should this rule apply to?

If the selector matches an element, the styles inside apply.
If it doesn’t match, the styles are ignored.

Example:

    p {
      color: blue;
    }

Meaning:
Select all `<p>` elements.

---

### 3. Declaration block — the “what to do” part

Everything inside `{}` is called the **declaration block**.

Inside it are **declarations**.

Each declaration follows this format:

    property: value;

Example:

    color: blue;
    font-size: 18px;

Rules:
- Property is always on the left
- Value is always on the right
- End with `;` (important habit)

---

### 4. Full example explained slowly

    p {
      color: blue;
      font-size: 18px;
    }

Plain English:
- Find every `<p>` element
- Make its text blue
- Make its text size 18 pixels

---

### 5. Simple selectors

#### Element selector
Targets HTML tag names.

    p { color: green; }
    h1 { font-size: 32px; }

---

#### Class selector
Targets elements with a class attribute.

    .highlight { background: yellow; }

HTML example:

    <p class="highlight">Hello</p>

---

#### ID selector
Targets one unique element.

    #header { padding: 20px; }

HTML:

    <div id="header"></div>

Rule:
IDs should be unique per page.

---

#### Universal selector
Targets everything.

    * { box-sizing: border-box; }

Use carefully; can be expensive.

---

### 6. Attribute selectors

Attribute selectors target elements based on attributes.

Examples:

Exact match:

    input[type="email"] { border-color: #888; }

Starts with:

    a[href^="https"] { color: green; }

Ends with:

    img[src$=".png"] { border: 1px solid #ccc; }

Contains:

    [title*="hello"] { text-decoration: underline; }

Real example:

    img[alt] { outline: 2px solid #ccc; }

Targets images that **have** an alt attribute.

---

### 7. Combinators — relationships between elements

Selectors can describe **relationships**.

#### Descendant (space)

    section p

Any `<p>` inside `<section>` (deep).

---

#### Child (>)

    ul > li

Only direct children.

---

#### Adjacent sibling (+)

    h2 + p

Only the paragraph immediately after an h2.

---

#### General sibling (~)

    h2 ~ p

All paragraphs after an h2 in the same parent.

---

### 8. Grouping selectors
---

Apply same styles to many selectors:

    h1, h2, h3 {
      font-family: Arial;
    }

Saves repetition.

---

### 9. Pseudo-classes — element states

Pseudo-classes style **states**, not elements.

Common ones:
- :hover
- :focus
- :active
- :visited

Structural:
- :first-child
- :last-child
- :nth-child(2)
- :nth-of-type(odd)

Examples:

    a:hover { text-decoration: underline; }

    .box:nth-child(2) { transform: scale(1.05); }

---

### 10. Pseudo-elements — parts of elements

Pseudo-elements style **parts** of elements.

Common:
- ::before
- ::after
- ::first-letter
- ::first-line

Example:

    h2::after {
      content: " ✨";
    }

Important:
::before and ::after need `content` to show.

---

### 11. Modern helper selectors

Exclude something:

    button:not(.primary)

Group without repetition:

    :is(h1, h2, h3)

Conditional parent selection (advanced):

    section:has(img)

Use :not and :is early.
Experiment with :has later.

---

### 12. Specificity & cascade — how conflicts are resolved

When multiple rules apply, the browser uses:

1. Importance
2. Specificity
3. Order

---

### 13. Specificity explained as scoring

Specificity is calculated as:

(a, b, c, d)

- a → inline styles
- b → ID selectors
- c → class, attribute, pseudo-class
- d → element, pseudo-element

Higher wins.

---

### 14. Specificity calculation example

Selector:

    header nav ul li a.active:hover

Breakdown:
- Inline → 0
- IDs → 0
- Classes/pseudo-classes → .active, :hover → 2
- Elements → header, nav, ul, li, a → 5

Score:
0*1000 + 0*100 + 2*10 + 5 = 25

---

### 15. Declarations — properties and values

A declaration is:

    property: value;

Properties:
- color
- margin
- display
- grid-gap

Values:
- keywords: block, center
- lengths: px, em, rem, %
- colors: #fff, rgb(), hsl()
- functions: calc(), var()
- URLs: url(...)

---

### 16. Units and value types

Pixels (px):
- Fixed size

em:
- Relative to element’s font size

rem:
- Relative to root font size

Percent (%):
- Relative to parent

Viewport:
- vw, vh (screen size)

Math:

    width: calc(100% - 40px);

---

### 17. Inheritance and defaults

Inherited:
- color
- font-family
- line-height

Not inherited:
- margin
- padding
- border

Special keywords:
- inherit
- initial
- unset

---

### 18. Shorthand properties

Examples:

    margin: 10px 20px;
    padding: 5px;
    border: 1px solid #000;

Warning:
Shorthands override longhand values.

---

### 19. CSS custom properties (variables)

Define:

    :root {
      --main: #1f8ef1;
      --pad: 12px;
    }

Use:

    background: var(--main);

Theme switching:

    [data-theme="dark"] {
      --bg: #111;
      --text: #eee;
    }

---

### 20. !important — last resort

    color: red !important;

Forces priority.
Avoid unless absolutely necessary.

---

### 21. At-rules — rules that control rules

At-rules start with `@`.

Examples:
- @media
- @keyframes
- @font-face
- @supports
- @import

---

### 22. Media queries — absolute beginner explanation

Media queries let CSS **change based on conditions**.

Most common condition:
Screen size.

Syntax:

    @media (condition) {
      CSS rules here
    }

Example:

    @media (max-width: 600px) {
      body { background: lightgray; }
    }

Meaning:
If screen width is 600px or less, apply these styles.

---

### 23. Media queries from scratch

Why needed:
- Mobile screens are small
- Desktop screens are large

Without media queries:
- Layout breaks on phones

With media queries:
- Layout adapts

---

### 24. Common media query conditions

Width:
- max-width
- min-width

Height:
- max-height
- min-height

Orientation:
- portrait
- landscape

---

### 25. Mobile-first vs desktop-first

Mobile-first (recommended):

    body { font-size: 14px; }

    @media (min-width: 768px) {
      body { font-size: 16px; }
    }

Start small, enhance upward.
