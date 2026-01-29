## Basic CSS Selectors

### 1. Big picture: four basic ways to point at elements

In CSS, selectors are how you say to the browser:

“Hey you, I want to style you.”

At the most basic level, there are **four core selectors** you will use all the time:

- Element selector  
- Class selector  
- ID selector  
- Universal selector `*`  

Everything else in CSS builds on top of these.

Think of them as different ways to **point your finger** at HTML elements.

---

### 2. Prerequisite: what does “select” mean?

To “select” in CSS simply means:

Choose which HTML elements should receive the styles.

Example:

    p {
      color: blue;
    }

This does **not** create paragraphs.
It only styles paragraphs that already exist in HTML.

---

### 3. Element selector — “select all of this tag”

#### What it is

The element selector targets **all HTML elements of a given tag name**.

Examples:

    p { color: blue; }
    h1 { font-size: 32px; }
    button { cursor: pointer; }

Meaning:
- `p` → all `<p>` elements
- `h1` → all `<h1>` elements
- `button` → all `<button>` elements

---

#### Strength

Element selectors are **weak** on purpose.

That’s good.

It means:
- You can easily override them later
- They are great for base styling

---

#### When to use element selectors

Use them for global, consistent rules:

    body { font-family: Arial, sans-serif; }
    p { line-height: 1.6; }
    h1, h2, h3 { font-weight: 600; }

---

#### Common pitfall

If you style elements too heavily:

    p {
      background: yellow;
      border: 3px solid red;
    }

You may regret it later because **every paragraph everywhere** is affected.

---

### 4. Class selector — “select elements with a label”

#### What a class is

A class is a **label** you add to HTML elements.

HTML:

    <p class="highlight">Important text</p>
    <button class="primary-btn">Save</button>

CSS:

    .highlight {
      background-color: yellow;
    }

    .primary-btn {
      background-color: blue;
      color: white;
    }

The dot `.` means:
“Select elements with this class.”

---

#### Classes are reusable

You can use the same class on many elements:

    <p class="highlight">Paragraph</p>
    <span class="highlight">Inline text</span>
    <div class="highlight">Box</div>

All of them get styled by:

    .highlight { background: yellow; }

---

#### One element can have many classes

This is very important.

HTML:

    <button class="btn primary large">Click me</button>

CSS:

    .btn {
      border-radius: 4px;
    }

    .primary {
      background: blue;
      color: white;
    }

    .large {
      padding: 12px 20px;
      font-size: 18px;
    }

All styles combine on the same element.

This is how real-world CSS is written.

---

#### Strength of class selectors

Class selectors are **stronger than element selectors**, but not too strong.

This makes them:
- Flexible
- Reusable
- Easy to manage

---

#### When to use classes

Use classes for **most of your styling**:

- Buttons
- Cards
- Alerts
- Form fields
- Layout blocks

---

#### Combining element + class

You can be more specific:

    p.highlight { color: red; }

This means:
- Only `<p>` elements
- That also have class `highlight`

---

### 5. ID selector — “select the one unique thing”

#### What an ID is

An ID is a **unique name** for one element.

HTML:

    <section id="typography">
      ...
    </section>

CSS:

    #typography {
      padding: 20px;
      background: #f7f7f7;
    }

The `#` means:
“Select the element with this id.”

---

#### Important rule: IDs must be unique

On a page, this is valid:

    <header id="main-header"></header>
    <footer id="main-footer"></footer>

This is NOT valid:

    <div id="box"></div>
    <div id="box"></div>

IDs are **not reusable** like classes.

---

#### Strength of ID selectors

ID selectors are **very strong**.

They override:
- Element selectors
- Class selectors

This makes them powerful, but dangerous.

---

#### When IDs are appropriate

Good uses:
- Unique page sections (header, footer)
- JavaScript hooks
- Anchor links

Example:

    #header
    #footer
    #main-content

---

#### Important best practice

For styling:
- Prefer classes

For identification or JavaScript:
- Use IDs

Why?
Because strong selectors are hard to override later.

Avoid:

    #save-button { background: blue; }

Prefer:

    .primary-btn { background: blue; }

---

### 6. Universal selector `*` — “select everything”

#### What it is

The universal selector matches **all elements**.

Example:

    * {
      box-sizing: border-box;
    }

This applies to:
- div
- p
- span
- button
- everything

---

#### Strength

The universal selector is **very weak**.

Almost anything overrides it.

That’s why it’s safe for defaults.

---

#### Common and useful use case: reset

Very common pattern:

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

This:
- Removes browser default spacing
- Makes sizing easier to reason about

---

#### Scoped universal selector

You can limit its effect:

    #form * {
      font-family: inherit;
    }

Meaning:
“All elements inside #form should inherit the font.”

Another example:

    .flex-container > * {
      margin-right: 10px;
    }

“All direct children get spacing.”

---

### 7. Comparing all four selectors together

HTML:

    <p id="msg" class="highlight">Hello!</p>

CSS:

    * { color: orange; }
    p { color: red; }
    .highlight { color: blue; }
    #msg { color: green; }

Result:
- `*` applies first
- `p` overrides it
- `.highlight` overrides that
- `#msg` wins

Final color: **green**

---

### 8. How to choose the right selector

- Use **element selectors** for base styling
- Use **class selectors** for most real styling
- Use **ID selectors** sparingly
- Use **universal selector** for resets or scoped rules

---

### 9. Common beginner mistakes

- Styling everything with IDs
- Overusing the universal selector
- Making element selectors too specific
- Forgetting that classes are reusable
- Mixing up class (`.`) and id (`#`)

---

### 10. Slightly advanced but still simple combinations

All of these still use only the four basics:

    nav a { ... }                 /* links inside nav */
    .flex-container > * { ... }   /* direct children */
    #typography p { ... }         /* paragraphs in section */
    .box.highlight { ... }        /* element with both classes */
    .error { ... }                /* any element with class error */

You will use these patterns constantly.

---

### 11. Final takeaway

These four selectors are your foundation:

- Element → broad, global
- Class → reusable, flexible (most important)
- ID → unique, strong (use carefully)
- `*` → global defaults and resets

