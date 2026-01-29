## Pseudo Classes

### 0. What is a pseudo-class?

A pseudo-class is a way to say:

“Select this element, but only when it is in a certain situation or state.”

So instead of styling an element all the time, you style it only when something specific is happening.

Examples of such states:

- The mouse is over it → :hover
- It is being clicked → :active
- It has keyboard focus → :focus
- It is the 2nd, 3rd, odd, even child → :nth-child()

You always attach a pseudo-class to a normal selector.

Examples:

    button:hover { ... }
    input:focus { ... }
    li:nth-child(2) { ... }

Think of it like:
“Select this element WHEN something is true.”

---

### 1. :hover — when the mouse is over the element

#### Core idea

:hover means:

“Apply these styles while the user’s mouse pointer is on top of the element.”

Example:

    button:hover {
      background-color: #1f8ef1;
      color: white;
    }

When the mouse enters the button → styles apply  
When the mouse leaves → styles stop applying

---

#### How to write :hover

Take any selector and add :hover:

    a:hover { ... }
    .nav-item:hover { ... }
    #header:hover { ... }

---

#### Using :hover example

Buttons:

    button {
      background: #eee;
      color: #333;
      border-radius: 4px;
      padding: 8px 12px;
      border: none;
      cursor: pointer;
    }

    button:hover {
      background: #ddd;
      transform: translateY(-2px);
    }

Navigation links:

    nav a {
      color: #555;
      text-decoration: none;
      padding: 4px 8px;
    }

    nav a:hover {
      color: #1f8ef1;
      text-decoration: underline;
    }

---

#### Hover and mobile devices

Touch screens do not really have “hover”.

Some mobile browsers simulate hover on tap, some do not.

Important rule:
Do not rely on :hover alone to show critical information or instructions.

Hover is best for:
- visual feedback
- decoration
- subtle animations

---

### 2. :active — when the element is being pressed

#### Core idea

:active means:

“Apply this style while the element is actively being pressed.”

This happens:
- after mouse button goes down
- before mouse button is released

Example:

    button:active {
      transform: translateY(1px);
      box-shadow: none;
    }

This gives a “pressed” or “sinking” effect.

---

#### Typical mouse sequence

1. Mouse moves over element → :hover
2. Mouse button pressed → :active (and usually still :hover)
3. Mouse button released → :active ends
4. Element may remain :hover
5. Element may receive :focus

---

#### Using :active example

    button {
      transition: transform 0.1s ease, box-shadow 0.1s ease;
      box-shadow: 0 2px 4px rgba(0,0,0,0.15);
    }

    button:active {
      transform: translateY(1px);
      box-shadow: 0 0 0 rgba(0,0,0,0.15);
    }

---

#### Extra notes about :active

- Works on buttons, links, inputs, etc.
- Can be triggered by keyboard (Enter or Space on focused buttons)

---

### 3. :focus — when the element has keyboard focus

#### Core idea

:focus means:

“This element is currently selected for interaction.”

This usually happens when:
- You tab to an element using the keyboard
- You click into an input field

Example:

    input:focus,
    textarea:focus {
      outline: 2px solid #1f8ef1;
      outline-offset: 2px;
    }

---

#### Using :focus example

Form fields:

    <input type="text">
    <input type="email">
    <textarea></textarea>

CSS:

    #form input:focus,
    #form textarea:focus,
    #form select:focus {
      outline: 2px solid #1f8ef1;
      outline-offset: 2px;
    }

---

#### Very important accessibility note

Many beginners do this:

    :focus {
      outline: none;
    }

This removes the visual indicator of focus.

Why this is bad:
- Keyboard users rely on focus to know where they are
- Without it, the site becomes very hard or impossible to use

Rule:
Never remove focus styles unless you replace them with a visible alternative.

Good pattern:

    :focus {
      outline: 2px solid #1f8ef1;
      outline-offset: 2px;
    }

---

### 3.1 :focus-visible — a smarter focus indicator

:focus-visible shows focus styles mainly for keyboard users.

Mouse users often won’t see it.

Pattern:

    :focus {
      outline: none;
    }

    :focus-visible {
      outline: 2px solid #1f8ef1;
      outline-offset: 2px;
    }

Result:
- Mouse clicks don’t show random outlines
- Keyboard navigation stays accessible

---

### 4. How :hover, :active, and :focus work together

For a clickable element like a button:

- Mouse over → :hover
- Mouse down → :hover + :active
- Mouse up → :active ends
- Button may stay :hover
- Button may receive :focus

For keyboard users:

- Tab to button → :focus
- Press Enter/Space → :active
- Release → :active ends, :focus remains

Example pattern:

    button {
      background: #eee;
    }

    button:hover {
      background: #ddd;
    }

    button:active {
      background: #ccc;
    }

    button:focus-visible {
      outline: 2px solid #1f8ef1;
    }

---

### 5. :nth-child() — selecting by position (deep dive)

This is one of the most powerful pseudo-classes.

We will go slowly.

---

### 5.1 Core idea of :nth-child()

:nth-child() selects elements based on their position among siblings.

Important rules:
- Counting starts at 1, not 0
- It counts all child elements, not just one tag type
- The selector must still match the element you write

Basic forms:

    li:nth-child(2)
    li:nth-child(odd)
    li:nth-child(even)
    li:nth-child(2n)
    li:nth-child(2n + 1)

---

### 5.2 Simple example

HTML:

    <ul>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
      <li>Item 4</li>
    </ul>

CSS:

    li:nth-child(1) { color: red; }
    li:nth-child(2) { color: blue; }
    li:nth-child(odd) { font-weight: bold; }
    li:nth-child(even) { text-decoration: underline; }

---

### 5.3 The math form: an + b

General form:

    :nth-child(an + b)

Where:
- a = step size
- n = 0, 1, 2, 3, ...
- b = starting offset

Example: :nth-child(2n)

    n = 0 → 0 (ignored)
    n = 1 → 2
    n = 2 → 4
    n = 3 → 6

Matches: 2, 4, 6, ...

Example: :nth-child(2n + 1)

    n = 0 → 1
    n = 1 → 3
    n = 2 → 5

Matches: 1, 3, 5, ...

Example: :nth-child(3n + 2)

Matches: 2, 5, 8, ...

---

### 5.4 Using :nth-child() example

Grid items:

    .grid-container .grid-item:nth-child(odd) {
      background-color: #f3f7ff;
    }

    .grid-container .grid-item:nth-child(even) {
      background-color: #eaf2ff;
    }

Table rows:

    #table table tr:nth-child(even) {
      background-color: #f9f9f9;
    }

    #table table tr:nth-child(1) {
      background-color: #ddd;
      font-weight: bold;
    }

---

### 5.5 :nth-child() vs :nth-of-type()

Common confusion.

HTML:

    <ul>
      <li>Item 1</li>
      <p>Paragraph</p>
      <li>Item 2</li>
    </ul>

Explanation:

- li:nth-child(2) → checks child 2 (p), so no li is selected
- li:nth-child(3) → selects Item 2

But:

    li:nth-of-type(2)

Counts only li elements:
- first li → 1
- second li → 2

So it selects Item 2.

If all siblings are the same type, both behave the same.

---

### 5.6 Negative values in :nth-child()

Example:

    li:nth-child(-n + 3) {
      font-weight: bold;
    }

Values:
- n = 0 → 3
- n = 1 → 2
- n = 2 → 1
- n = 3 → 0 (ignored)

Result:
First 3 children are selected.

Rule:
When the result is 0 or less, it is ignored.

---

### 6. Specificity of pseudo-classes

All pseudo-classes:
- :hover
- :active
- :focus
- :nth-child()
- :focus-visible

Have the same specificity level as a class selector.

Examples:

    button:hover
    li:nth-child(2)

Each one adds class-level specificity to the selector.

