## Pseudo Elements

### 1. What is a pseudo-element?

Think of a pseudo-element like this:

“A fake part of an element that does not exist in HTML, but CSS pretends it exists so you can style it.”

It is attached to a real element, but it is not a real tag in the HTML.

Common pseudo-elements:

- ::before → a virtual box before the element’s content
- ::after → a virtual box after the element’s content
- ::first-letter → the first letter of a block of text
- ::first-line → the first line of text
- ::selection → the highlighted text when the user selects text

How they are written:

    selector::pseudo-element { ... }

Examples:

    button::before { ... }
    p::first-letter { ... }

They always belong to a real element, but they themselves are not real HTML elements.

---

### 2. ::before and ::after — the most important pseudo-elements

These two are used everywhere in modern CSS.

They create **generated content**, meaning content created by CSS, not written in HTML.

---

### 2.1 Basic rules for ::before and ::after

To use ::before or ::after correctly, you must follow these rules:

1. You need a normal selector (button, p, .card, etc.)
2. You must define the content property (even if it is an empty string)
3. You can style them like small elements (width, height, color, position, etc.)

Example:

    button::before {
      content: "★ ";
    }

This visually adds a star before the button text.

If you forget the content property, the pseudo-element will not appear.

---

### 2.2 ::before — content before the element’s text

Simple example:

    p::before {
      content: "👉 ";
    }

HTML:

    <p>Click this link</p>

Visual result:

👉 Click this link

Important note:
The arrow is not added to the HTML. It only exists visually.

Common uses for ::before:

- Decorative icons
- Small labels
- Custom bullets
- Background overlays

Example:

    section > h2::before {
      content: "◆ ";
      color: #1f8ef1;
    }

All section headings get a blue diamond before the text.

---

### 2.3 ::after — content after the element’s text

Same idea as ::before, but placed after the content.

Example:

    a::after {
      content: " ↗";
    }

This can visually mark external links.

Another example:

    button::after {
      content: " »";
    }

HTML:

    <button>Next</button>

Visual result:

Next »

---

### 2.4 Using ::before and ::after as shapes, not text

Pseudo-elements are not limited to text.

You can create shapes using width, height, background, and positioning.

Example: decorative underline

    .button-with-line {
      position: relative;
      padding-bottom: 10px;
    }

    .button-with-line::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0;
      width: 100%;
      height: 3px;
      background: #1f8ef1;
    }

This creates a line under the button text.

---

### 2.5 Hover underline effect using pseudo-elements

Common real-world pattern for navigation links:

    nav a {
      position: relative;
      text-decoration: none;
      padding: 4px 0;
    }

    nav a::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: -2px;
      width: 0;
      height: 2px;
      background: #1f8ef1;
      transition: width 0.2s ease;
    }

    nav a:hover::after {
      width: 100%;
    }

This creates a smooth “growing underline” on hover.

---

### 2.6 Combining pseudo-classes with pseudo-elements

You can combine them like this:

    button:hover::before {
      content: "🔥 ";
    }

Meaning:
“When the button is hovered, show this before-content.”

Common pattern for show/hide effects:

    button::before {
      content: "";
      opacity: 0;
      transition: opacity 0.2s ease;
    }

    button:hover::before {
      opacity: 1;
    }

---

### 2.7 Practical example

Primary button with an icon:

    .primary-btn {
      position: relative;
      padding-left: 24px;
    }

    .primary-btn::before {
      content: "★";
      position: absolute;
      left: 8px;
      top: 50%;
      transform: translateY(-50%);
      opacity: 0.5;
    }

Danger button warning on hover:

    .danger-btn:hover::before {
      content: "⚠ ";
    }

---

### 2.8 Positioning and layout with pseudo-elements

By default, ::before and ::after behave like inline text.

For layouts and decorations, the most common pattern is:

- Parent → position: relative
- Pseudo-element → position: absolute

Example: card overlay

    .card {
      position: relative;
    }

    .card::before {
      content: "";
      position: absolute;
      inset: 0;
      background: rgba(0, 0, 0, 0.3);
    }

This creates a semi-transparent overlay over the card.

---

### 2.9 Important limitations of ::before and ::after

- You cannot insert real HTML elements
- content: "<span>Hi</span>" will show text, not a real span
- Images must be added using background-image, not <img>
- Some elements like input or img may not support pseudo-elements reliably

For form inputs, use wrappers:

    <div class="input-wrapper">
      <input type="text">
    </div>

    .input-wrapper {
      position: relative;
    }

    .input-wrapper::before {
      content: "🔍";
      position: absolute;
      left: 8px;
      top: 50%;
      transform: translateY(-50%);
    }

---

### 3. ::first-letter — styling the first letter

Simple idea:

“Style only the very first letter of a block of text.”

Classic use: drop caps.

Example:

    p::first-letter {
      font-size: 2.5em;
      font-weight: bold;
      float: left;
      margin-right: 8px;
    }

Notes:

- Works on block-level text elements
- The browser decides what counts as the first letter
- Only certain properties apply

Example:

    #typography p::first-letter {
      font-size: 2em;
      font-weight: bold;
      color: #1f8ef1;
    }

---

### 4. ::first-line — styling the first line of text

Simple idea:

“Style the first visible line of text.”

Important:
The first line depends on layout and width.

Example:

    p::first-line {
      font-weight: bold;
      text-transform: uppercase;
    }

Notes:

- Only text-related properties apply
- Margin, padding, and layout properties do not work
- Resizing the window can change which text is the first line

Example:

    #typography p::first-line {
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }

---

### 5. ::selection — styling selected text

Simple idea:

“Style the text when the user selects it.”

Example:

    ::selection {
      background: #1f8ef1;
      color: white;
    }

Targeting specific elements:

    p::selection {
      background: #ffeb3b;
      color: #000;
    }

Notes:

- Only a few properties are allowed
- This is purely visual
- Behavior may vary slightly between browsers

Example:

    body::selection {
      background: #ffe082;
      color: #000;
    }

---

### 6. Combining pseudo-elements with other selectors

You can combine pseudo-elements with:

- pseudo-classes
- position selectors
- state selectors

Example:

    button::before {
      content: "";
      position: absolute;
      inset: 0;
      border-radius: inherit;
      border: 2px solid transparent;
      transition: border-color 0.2s ease;
    }

    button:hover::before {
      border-color: #1f8ef1;
    }

Example with nth-child:

    .grid-item:nth-child(3)::before {
      content: "★ ";
      color: gold;
    }

Only the third grid item gets a star.

---

### 7. Specificity of pseudo-elements

Pseudo-elements behave like element selectors in specificity.

Examples:

    button::before
    p::first-letter

They do not significantly increase specificity.

Example comparison:

- button → element
- button::before → element-level
- button.primary::before → element + class

---

### 8. Gotchas and best practices

#### 8.1 Always define content

This will not work:

    .box::after {
      width: 10px;
      height: 10px;
      background: red;
    }

This will work:

    .box::after {
      content: "";
      width: 10px;
      height: 10px;
      background: red;
    }

---

#### 8.2 Do not use pseudo-elements for critical text

Because pseudo-element content is not real HTML:

- Screen readers may not announce it
- It may not be accessible

Do not use it for:
- Error messages
- Required labels
- Important instructions

Use real HTML for important content.

---

#### 8.3 Replaced elements warning

Elements like img, input, textarea are replaced elements.

Pseudo-elements may not behave consistently on them.

Use wrapper elements when needed.

---

### 9. Final mental model

Pseudo-elements let you:

- Add decoration without extra HTML
- Create visual effects cleanly
- Keep markup simple and semantic

Use them for:
- Icons
- Underlines
- Overlays
- Decorative labels

Avoid them for:
- Essential content
- Meaningful text

Once you understand ::before and ::after, you unlock a huge part of modern CSS styling power.
