## CSS Box Model

### 1. The CSS Box Model – the mental image

Imagine every HTML element as a rectangular box made of layers.

From inside to outside:

- Content → the actual thing (text, image, child elements)
- Padding → space inside the box, around the content
- Border → the visible edge of the box
- Margin → space outside the box, pushing other elements away

A simple way to remember:

- Content = the thing
- Padding = breathing room inside
- Border = the box edge
- Margin = distance from other boxes

---

### 2. Content

Content is what you actually put in HTML.

Example:

    <div class="card">
      Hello world
    </div>

If you write:

    .card {
      width: 200px;
      height: 100px;
    }

That 200 by 100 applies to the content area by default.

Inside this content area:
- Text wraps based on width and font size
- Images take space
- Child elements live here

At this point, there is no space between content and the edge unless you add padding.

---

### 3. Padding – space inside the box

Padding pushes the content away from the border.

Example:

    .card {
      padding: 20px;
    }

This adds 20px of space on all sides inside the box.

Padding shorthand rules:

    padding: 10px;
    padding: 10px 20px;
    padding: 10px 20px 30px;
    padding: 10px 20px 30px 40px;

Meaning:

- 1 value → all sides
- 2 values → top/bottom, left/right
- 3 values → top, left/right, bottom
- 4 values → top, right, bottom, left (clockwise)

Important points about padding:

- Padding adds to the total size when using the default box-sizing
- Background color extends into padding
- Padding is inside the border

---

### 4. Border – the visible edge

Border wraps around padding and content.

Example:

    .card {
      border: 2px solid black;
    }

Border shorthand:

    border: width style color;

Examples:

    border: 1px solid #ccc;
    border: 4px dashed red;
    border: 0;

You can control sides individually:

    border-top: 2px solid red;
    border-right: none;

With the default box-sizing, border also adds to the total size.

---

### 5. Margin – space outside the box

Margin creates space between elements.

Example:

    .card {
      margin: 20px;
    }

Margin characteristics:

- Outside the border
- Transparent (no background)
- Pushes other elements away
- Not part of the element’s own box

Margin shorthand follows the same pattern as padding:

    margin: 10px;
    margin: 10px 20px;
    margin: 10px 20px 30px;
    margin: 10px 20px 30px 40px;

---

### 6. Margin auto – centering elements

Very common pattern:

    .container {
      width: 600px;
      margin: 0 auto;
    }

What this means:

- Top and bottom margin = 0
- Left and right margin = auto

For a block element with a fixed width, this centers it horizontally.

---

### 7. How total size is calculated (default box-sizing)

By default, most elements use:

    box-sizing: content-box;

This means:
- width and height apply only to content
- padding and border are added on top

Formula for total width:

- margin-left
- border-left
- padding-left
- content width
- padding-right
- border-right
- margin-right

---

### 8. Example: calculate total size step by step

Example:

    .box {
      width: 200px;
      padding: 10px;
      border: 2px solid black;
      margin: 15px;
    }

Horizontal calculation:

- Content width = 200
- Padding left + right = 10 + 10 = 20
- Border left + right = 2 + 2 = 4
- Margin left + right = 15 + 15 = 30

Now add carefully:

- Content + padding = 200 + 20 = 220
- border = 220 + 4 = 224
- margin = 224 + 30 = 254

So the element occupies 254px horizontally in the layout.

---

### 9. box-sizing: border-box – the practical default

Most developers prefer:

    *,
    *::before,
    *::after {
      box-sizing: border-box;
    }

With border-box:

- width includes content + padding + border
- padding and border are taken out of the content area
- total width stays predictable

Example:

    .box {
      width: 200px;
      padding: 10px;
      border: 2px solid black;
      box-sizing: border-box;
    }

Total width = exactly 200px.

Internal math:

- Border left + right = 2 + 2 = 4
- Padding left + right = 10 + 10 = 20
- Content width = 200 − 24 = 176px

You usually do not care about content width here.
What matters is:
“The whole box stays 200px wide.”

That’s why border-box is easier for layouts.

---

### 10. Margin collapsing – the tricky part

This is the most confusing part of the box model.

Margin collapsing happens only with vertical margins (top and bottom).

Instead of adding margins together, the browser uses the larger one.

---

### 10.1 Margin collapse between siblings

HTML:

    <p class="one">Paragraph 1</p>
    <p class="two">Paragraph 2</p>

CSS:

    .one {
      margin-bottom: 30px;
    }

    .two {
      margin-top: 20px;
    }

You might expect 50px space.
Actual result: 30px.

Why?
Because the margins touch and collapse.
The browser uses max(30, 20).

---

### 10.2 Margin collapse between parent and child

HTML:

    <div class="parent">
      <p class="child">Hello</p>
    </div>

CSS:

    .parent {
      background: lightyellow;
    }

    .child {
      margin-top: 30px;
    }

You might expect:
- 30px space inside the parent above the text

What actually happens:
- The parent itself moves down by 30px

This is parent–child margin collapse.

It happens when:
- Parent has no border-top
- No padding-top
- No inline content before the child

---

### 10.3 When margins do NOT collapse

Margins do not collapse if:

- There is padding or border between elements
- The element creates a new layout context (flex, grid, overflow)
- The element is positioned (absolute or fixed)
- Margins are left/right (horizontal margins never collapse)

Ways to stop parent–child collapse:

    .parent {
      padding-top: 1px;
    }

or

    .parent {
      border-top: 1px solid transparent;
    }

or

    .parent {
      overflow: auto;
    }

---

### 11. Border vs Outline – common confusion

#### Border

- Part of the box model
- Sits between padding and margin
- Affects layout
- Can be per side
- Can be rounded

Example:

    button {
      border: 2px solid #1f8ef1;
    }

#### Outline

- Not part of the box model
- Drawn outside the border
- Does not affect layout
- Same on all sides
- Can be offset

Example:

    button:focus {
      outline: 3px solid #1f8ef1;
      outline-offset: 2px;
    }

---

### 12. Why outlines are used for focus

Browsers use outlines for focus because:

- They are visible
- They do not shift layout
- They work well for accessibility

Custom example:

    button:focus-visible {
      outline: 2px solid #1f8ef1;
      outline-offset: 3px;
    }

Do not remove focus outlines unless you replace them with something visible.

---

### 13. Border vs Outline – quick comparison

- Border is part of the box model and affects size
- Outline is outside the box and does not affect size
- Border is for visual structure
- Outline is mainly for focus and accessibility

---

### 14. Final mental model

When you look at any element, think:

- What is the content?
- How much padding does it have?
- Does the border add size?
- How do margins interact with neighbors?
- Is box-sizing content-box or border-box?
