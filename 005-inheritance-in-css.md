## Inheritance in CSS

### 1. Big idea: what “inheritance” means in CSS

Inheritance in CSS means:

Some style values automatically pass from a parent element to its child elements.

Think of it like family traits.

If a parent sets something like text color or font:
- Children usually get the same text color or font
- Unless they explicitly change it

So instead of repeating styles everywhere, CSS lets some values **flow downward**.

---

### 2. Very basic prerequisite: parent and child elements

Before understanding inheritance, you must know this:

HTML elements are nested.

Example:

    <div>
      <p>Hello</p>
    </div>

Here:
- `div` is the parent
- `p` is the child

Inheritance always works **from parent → child**, never the other way around.

---

### 3. First simple example of inheritance

CSS:

    body {
      color: #333;
    }

HTML:

    <body>
      <p>Hello</p>
      <span>World</span>
    </body>

What happens:
- The body text color is set to #333
- The paragraph and span automatically use the same color

Why?
Because **color is an inherited property**.

You did not style `p` or `span`, but they still got the color.

---

### 4. Important rule: not everything is inherited

This is critical for beginners:

Some CSS properties inherit.
Some do not.

Inheritance is **property-specific**, not automatic for everything.

If you assume everything inherits, CSS will feel confusing.

---

### 5. Common properties that DO inherit

These usually pass from parent to child:

- color
- font-family
- font-size
- font-style
- font-weight
- line-height
- text-align
- visibility

Example:

    body {
      font-family: Arial;
      color: black;
    }

All text inside the page uses Arial and black by default.

---

### 6. Common properties that do NOT inherit

These usually do NOT pass down:

- margin
- padding
- border
- width
- height
- background
- display
- position

Example:

    div {
      padding: 20px;
    }

Child elements do NOT automatically get padding.

Each element controls its own spacing and layout.

---

### 7. Why CSS is designed this way

Text-related properties inherit because:
- Consistent typography is important
- Repeating font rules everywhere would be painful

Layout-related properties do NOT inherit because:
- Each element needs independent size and position
- Inheriting layout would break designs

This separation is intentional.

---

### 8. Overriding inherited values

A child can override inherited styles easily.

Example:

    body {
      color: black;
    }

    p {
      color: red;
    }

Result:
- Body text is black
- Paragraph text is red

Explicit rules always override inherited ones.

---

### 9. The inherit keyword

Sometimes you want a property to inherit even if it normally doesn’t.

You can force it using:

    inherit

Example:

    button {
      color: inherit;
    }

Meaning:
- Take the text color from the parent

This is very common for buttons and links.

---

### 10. The initial keyword 

`initial` means:
Reset the property to the browser’s default value.

Example:

    p {
      color: initial;
    }

Even if the parent set a color, this paragraph goes back to default.

Useful when undoing inherited styles.

---

### 11. The unset keyword

`unset` behaves differently depending on the property.

- If the property normally inherits → behaves like inherit
- If the property does not inherit → behaves like initial

Example:

    p {
      color: unset;
    }

This adapts automatically.

---

### 12. Inheritance vs grouping

Inheritance:

    body {
      color: black;
    }

Grouping:

    p, span, a {
      color: black;
    }

Difference:
- Inheritance flows automatically
- Grouping explicitly targets elements

Inheritance is usually cleaner and more flexible.

---

### 13. Inheritance and links

Links often don’t look inherited.

Why?
Because browsers give links their own default styles.

Example:

    body {
      color: black;
    }

Links might still appear blue.

Fix:

    a {
      color: inherit;
    }

Now links follow the parent text color.

---

### 14. Inheritance and form elements

Inputs, buttons, and selects often ignore inheritance.

Example:

    body {
      font-family: Arial;
    }

Inputs may still look different.

Fix:

    input, button, textarea {
      font-family: inherit;
    }

Form elements often need explicit inheritance.

---

### 15. Inheritance and nesting depth

Inheritance continues down the tree:

    body → div → section → p → span

If no rule interrupts the chain:
- The value keeps flowing

If any element overrides it:
- Children inherit the new value instead

---

### 16. Advanced idea

When inheritance happens, the browser calculates the final value.

Example:

    body {
      font-size: 16px;
    }

    p {
      font-size: 1.2em;
    }

Here:
- The paragraph inherits font-size context
- Then adjusts it

You don’t need to know internal math.
Just know inheritance sets the base.

---

### 17. Inheritance and CSS variables

Variables inherit by default.

Example:

    body {
      --main-color: blue;
    }

    p {
      color: var(--main-color);
    }

Change the variable on a parent:
- All children update automatically

This is powerful for theming.

---

### 18. Common beginner mistakes with inheritance

- Expecting margin or padding to inherit
- Forgetting that links have default styles
- Overriding inherited styles accidentally
- Using inline styles that block inheritance
- Not using inherit when needed

---

### 19. Practical best practices

- Set typography on body or root elements
- Let inheritance do the work
- Override only where needed
- Use inherit for buttons and links
- Avoid repeating font and color rules everywhere

---

### 20. Simple mental model to remember

Ask two questions:

1. Is this a text-related property?
   → Probably inherits

2. Is this a layout or spacing property?
   → Probably does not inherit

This rule alone prevents most confusion.

---

### 21. Final takeaway

Inheritance is CSS’s way of reducing repetition.

It:
- Makes styles consistent
- Keeps CSS cleaner
- Helps large sites stay maintainable

