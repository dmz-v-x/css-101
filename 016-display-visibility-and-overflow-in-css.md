## Display, Visibility, and Overflow in CSS 

### 0. Big Picture – What does display control?

The display property decides:

- How an element behaves in layout
- Whether it starts on a new line
- Whether it stretches across width
- Whether it sits inside a line of text
- What layout rules apply to its children

Simple mental model:

display = role of the element in the layout

Different HTML elements have default roles:

- div, p, h1, section → block
- span, a, strong → inline
- button, input → inline-block (roughly)
- ul, ol → block
- img → behaves like inline-block-ish

CSS lets you change that role.

---

### 1. display: block

Simple definition:

A block element behaves like a full-width row.

Key behaviors:

- Starts on a new line
- Stacks vertically
- Stretches to fill available width (by default)
- Height grows with content

You can control:

- width
- height
- margin (all sides)
- padding
- border

Example:

    .card {
      display: block;
      width: 300px;
      margin: 16px auto;
      padding: 16px;
      border: 1px solid #ccc;
    }

This element:

- Sits on its own line
- Has fixed width
- Can be centered
- Acts like a layout container

Most layout containers are block elements.

---

### 2. display: inline

Simple definition:

An inline element behaves like a word in a sentence.

Key behaviors:

- Does NOT start a new line
- Sits next to text
- Size depends on content
- width & height mostly ignored

Important quirks:

- margin-left/right works
- margin-top/bottom usually ineffective
- padding-top/bottom affects visuals but not layout spacing

Example:

    .highlight {
      display: inline;
      background: yellow;
      padding: 2px 4px;
    }

Used for:

- Styling parts of text
- Small labels
- Inline decorations

Inline is NOT for layout boxes.

---

### 3. display: inline-block

Simple definition:

Inline-block = inline behavior + block features

Meaning:

- Sits inline like text
- BUT acts like a box

You can set:

- width
- height
- margin
- padding
- border

Example:

    .badge {
      display: inline-block;
      background: #1f8ef1;
      color: white;
      padding: 4px 8px;
      border-radius: 12px;
    }

Perfect for:

- Badges
- Pills
- Small UI components
- Menu items

---

### 4. display: none

Simple definition:

The element is removed from the page visually.

Key effects:

- Not visible
- Takes NO space
- Layout ignores it
- Not interactive

Example:

    .hidden {
      display: none;
    }

Difference from visibility:

display: none → element gone  
visibility: hidden → element invisible but space remains

---

### 5. display: flex (high-level)

Makes element a flex container.

Children become flex items.

Example:

    .flex-container {
      display: flex;
      gap: 16px;
    }

Flexbox is great for:

- Rows
- Columns
- Alignment
- Spacing
- Responsive components

Think:

flex = one direction layout

---

### 6. display: grid (high-level)

Makes element a grid container.

Example:

    .grid-container {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 12px;
    }

Grid is great for:

- Rows + columns
- Complex layouts
- Dashboards
- Galleries

Think:

grid = two direction layout

---

### 7. visibility – Hide but keep space

visibility controls visibility only.

Example:

    .box.hidden {
      visibility: hidden;
    }

Effects:

- Element invisible
- Space still exists
- Layout unchanged

---

### visibility vs display: none

display: none  
- Invisible  
- No space  

visibility: hidden  
- Invisible  
- Space kept  

Use visibility when layout stability matters.

---

### 8. overflow – What if content doesn’t fit?

overflow decides what happens when content is larger than box.

Example box:

    .box {
      width: 200px;
      height: 100px;
      border: 1px solid black;
    }

---

### 8.1 overflow: visible (default)

Content spills outside.

Usually undesirable.

---

### 8.2 overflow: hidden

Extra content clipped.

Useful for:

- Cropping
- Masks
- Animations
- Rounded image containers

Example:

    .image-wrapper {
      width: 150px;
      height: 150px;
      border-radius: 50%;
      overflow: hidden;
    }

---

### 8.3 overflow: scroll

Always shows scrollbars.

Even if unnecessary.

---

### 8.4 overflow: auto

Scrollbars only when needed.

Most common choice.

Example:

    .chat-window {
      height: 300px;
      overflow: auto;
    }

---

### 8.5 overflow-x / overflow-y

Control axes separately.

Example:

    .table-wrapper {
      overflow-x: auto;
      overflow-y: hidden;
    }

Perfect for wide tables.

---

### 9. Overflow affects layout behavior

Important insight:

overflow can change layout behavior.

Example:

    .parent {
      overflow: auto;
    }

This prevents margin collapsing with children.

You already saw this earlier.

---

### 10. How to build intuition (DevTools Tip)

Open DevTools → Inspect element → Toggle:

- block / inline / inline-block
- none
- flex / grid
- overflow values

Watch layout change live.

This is extremely powerful for learning.

---

### 11. Quick Cheat-Sheet

display:

block  
- New line  
- Full width  
- Layout containers  

inline  
- Same line  
- Content-sized  
- Text styling  

inline-block  
- Same line  
- Box-like  
- UI components  

none  
- Removed from layout  

flex  
- One-direction layout  

grid  
- Two-direction layout  

visibility:

visible → normal  
hidden → invisible but space kept  

overflow:

visible → spill out  
hidden → clip  
scroll → always scrollbar  
auto → scrollbar if needed  
overflow-x/y → axis control
