## Combinators & Advanced Selectors

### 0. Big picture: what are combinators and advanced selectors?

Let’s start from absolute zero.

A selector is how CSS tells the browser:
“Which HTML elements should I style?”

Examples you already know:

- p → all paragraphs
- .btn → elements with class btn
- #header → element with id header
- h1, h2 → grouped selectors

A combinator is a symbol placed between selectors that explains how two elements are related.

Advanced selectors are just more powerful ways to select elements based on:
- relationships between elements
- position in the HTML structure
- attributes like type or href
- user interaction like hover or focus

You already know:
- Descendant selector (space): A B
- Child selector (>): A > B

Now we will add:
- Sibling selectors: + and ~
- Attribute selectors: [type="email"], etc.
- Modern helpers: :not(), :is(), :where(), :has()

Everything is explained from zero to advanced, step by step.

### 1. Combinators: how selectors connect elements

HTML elements form a tree, like a family.

Elements can be:
- parents
- children
- siblings (same parent)

CSS combinators describe these relationships.

There are four main combinators:

- Descendant → A B
- Child → A > B
- Adjacent sibling → A + B
- General sibling → A ~ B

### 1.1 Descendant combinator — A B (space)

Meaning:
Select element B anywhere inside element A, no matter how deep.

Example 1:

    section p {
      color: blue;
    }

All paragraphs inside sections become blue.

Example 2: 

    #typography p {
      color: #333;
    }

Every paragraph inside the typography section is styled, even nested ones.

### 1.2 Child combinator — A > B

Meaning:
Select element B only if it is a direct child of element A.

Example 1:

    ul > li {
      list-style-type: square;
    }

Only list items directly inside the ul are affected.

Example 2:

    .flex-container > .box {
      border: 1px solid #ddd;
    }

Only boxes directly inside the flex container are selected.

### 2. Sibling selectors: elements next to each other

Sibling elements:
- share the same parent
- appear at the same level in HTML

There are two sibling selectors:
- + adjacent sibling
- ~ general sibling

### 2.1 Adjacent sibling selector — A + B

Meaning:
Select element B only if it comes immediately after element A.

HTML:

    <h2>Title</h2>
    <p>First paragraph</p>
    <p>Second paragraph</p>

CSS:

    h2 + p {
      font-weight: bold;
    }

Only the first paragraph becomes bold.
The second paragraph is ignored.

Practical example:

    <h2>Form Elements</h2>
    <p class="note">All fields are required.</p>
    <form>...</form>

    h2 + p {
      color: #777;
      font-style: italic;
    }

Only the note paragraph is styled.

### 2.2 General sibling selector — A ~ B

Meaning:
Select all B elements that come after A and share the same parent.

HTML:

    <h2>Title</h2>
    <p>First</p>
    <p>Second</p>
    <p>Third</p>

CSS:

    h2 ~ p {
      color: teal;
    }

All paragraphs after the h2 become teal.

Difference summary:
- A + B → only the first matching sibling
- A ~ B → all matching siblings after

### 2.3 Common real-world uses of sibling selectors

First paragraph after a heading:

    h2 + p {
      margin-top: 0;
    }

Checkbox label styling:

    input:checked + label {
      font-weight: bold;
    }

Notes after alerts:

    .alert ~ .note {
      opacity: 0.7;
    }

### 3. Attribute selectors — selecting by attributes

Attribute selectors let you style elements based on HTML attributes.

### 3.1 Basic attribute selector forms

Has attribute:

    [disabled] {
      opacity: 0.6;
    }

Exact value:

    input[type="email"] {
      border-color: steelblue;
    }

Contains word:

    [class~="error"] {
      color: red;
    }

Starts with:

    a[href^="https://"] {
      color: green;
    }

Ends with:

    img[src$=".png"] {
      border: 1px solid #ccc;
    }

Contains substring:

    a[href*="login"] {
      font-weight: bold;
    }

Language prefix:

    [lang|="en"] {
      font-style: italic;
    }

### 3.2 Combining attribute selectors

Examples:

    #form input[required] { ... }
    button[type="submit"] { ... }
    nav a[href^="#"] { ... }

From your scaffold:

    input[type="checkbox"],
    input[type="radio"] {
      width: 16px;
      height: 16px;
    }

### 3.3 Specificity note

Attribute selectors behave like class selectors in strength.

    input[type="text"]

Counts like:
- element (input)
- class-level ([type="text"])

### 4. Advanced but useful pseudo-classes

### 4.1 Position-based selectors

Examples:

    :first-child
    :last-child
    :nth-child(2)
    :nth-child(odd)
    :nth-of-type(3)

Examples:

    tr:nth-child(even) {
      background-color: #f9f9f9;
    }

### 4.2 Interaction-based selectors

Examples:

    button:hover {
      transform: translateY(-2px);
    }

    input:focus {
      outline: 2px solid #1f8ef1;
    }

### 4.3 Logic helpers

Exclude elements:

    button:not(.primary-btn) {
      background: #eee;
    }

Match any:

    :is(h1, h2, h3) {
      font-family: system-ui;
    }

Low-specificity match:

    :where(h1, h2, h3) {
      margin: 0;
    }

### 4.4 Parent-aware selector: :has()

Select parent if it contains something.

    .card:has(.error) {
      border-color: red;
    }

Form example:

    label:has(input:checked) {
      font-weight: bold;
    }

### 5. Realistic combinations from your HTML

First paragraph after section heading:

    section > h2 + p {
      font-style: italic;
      color: #666;
    }

Required form fields:

    #form input[required],
    #form textarea[required] {
      border: 1px solid #e67e22;
    }

Zebra striping tables:

    #table table tr:nth-child(even) {
      background-color: #f9f9f9;
    }

Text-like inputs grouped:

    #form :is(input[type="text"], input[type="email"], textarea) {
      width: 100%;
      padding: 8px;
    }

### 6. Final mental model

Think in layers:

1. What element?
2. How is it related to others?
3. Does it have a specific attribute or state?
4. Can logic help simplify this?

If you understand:
- A B
- A > B
- A + B
- A ~ B
