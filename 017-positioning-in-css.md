## CSS Positioning

### 0. Before Everything – Normal Flow

Let’s start from the natural behavior of a webpage.

Imagine a Word document:

- Block elements stack vertically
- Inline elements flow left → right inside lines

This default layout behavior is called **normal document flow**.

By default:

    position: static;

Most elements live happily here.

Positioning in CSS is basically asking:

“Should this element follow normal flow, or behave differently?”

---

### 1. position: static – The Default

    .element {
      position: static;
    }

This is the default.

Behavior:

- Element stays in normal flow
- top / left / right / bottom → ignored
- z-index → ignored

Think:

“Place me where I naturally belong.”

You almost never write this explicitly.

---

### 2. position: relative – Same Spot, But Shiftable

    .element {
      position: relative;
      top: 10px;
      left: 20px;
    }

Two critical ideas:

1. The element **still occupies its original space**
2. Offsets move the **visual box only**

Meaning:

Layout thinks element did not move.

But visually → it shifts.

Example logic:

Normal position → (0, 100)

After relative:

Layout → still (0, 100)  
Painting → (20, 110)

Other elements do NOT move to fill gaps.

---

#### Why relative is extremely important

It creates a **reference point** for absolute children.

    .parent {
      position: relative;
    }

    .child {
      position: absolute;
      top: 0;
      right: 0;
    }

Now child positions relative to parent.

Without relative → child may jump to viewport.

---

### 3. position: absolute – Removed from Flow

    .element {
      position: absolute;
      top: 20px;
      left: 30px;
    }

Key behavior:

- Removed from normal flow
- Takes NO space
- Floats above layout

Positioning reference:

Nearest ancestor with:

- relative
- absolute
- fixed
- sticky

If none → viewport

---

#### Example: Badge inside Card

    .card {
      position: relative;
    }

    .badge {
      position: absolute;
      top: 8px;
      right: 8px;
    }

Badge anchors nicely.

---

#### Stretching absolute elements

    .overlay {
      position: absolute;
      inset: 0;
    }

Equivalent to:

top: 0; right: 0; bottom: 0; left: 0;

Fills container.

---

### 4. position: fixed – Attached to Viewport

    .header {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
    }

Behaves like absolute BUT:

- Reference = viewport
- Does NOT move on scroll

Used for:

- Navbars
- Floating buttons
- Chat widgets

---

#### Classic Fixed Header Adjustment

    main {
      padding-top: 60px;
    }

Prevents content hiding.

---

### 5. position: sticky – Smart Hybrid

    .title {
      position: sticky;
      top: 0;
    }

Sticky behaves like:

- relative initially
- fixed when scrolled past threshold

Requirements:

- Must specify top / bottom / etc.
- Container must be tall enough

Sticky stays **within its container**, unlike fixed.

---

#### Why sticky sometimes “fails”

Common reasons:

- No top value
- Container too small
- Parent overflow interfering

---

### 6. Offsets – top, left, right, bottom

Behavior depends on position.

---

#### Static → Ignored

---

#### Relative → Shift from Normal Spot

    top: 10px → move DOWN  
    left: 20px → move RIGHT  

Space remains unchanged.

---

#### Absolute / Fixed → Distance from Reference Edges

    top: 0;
    right: 0;

Top-right corner.

---

#### Stretching trick

    left: 0;
    right: 0;

Full width.

---

#### Modern shorthand: inset

    inset: 10px;

All sides.

---

### 7. z-index – Who Sits on Top?

Used when elements overlap.

Works ONLY on positioned elements.

    .box {
      position: relative;
      z-index: 10;
    }

Rules:

Higher number → drawn on top

Example:

    .box1 { z-index: 1; }
    .box2 { z-index: 2; }

box2 wins.

---

#### Negative z-index

Possible but dangerous.

Can hide behind backgrounds.

---

### 8. Stacking Context – Advanced but Essential

This is where many developers get confused.

Think:

A stacking context = separate layering world.

Inside it:

- z-index works normally
- But children cannot escape parent’s layer

---

#### How stacking contexts form

Most important trigger:

positioned element + z-index

    .parent {
      position: relative;
      z-index: 10;
    }

Creates new stacking context.

---

#### Critical Example

    .parent { z-index: 10; }
    .child  { z-index: 9999; }
    .sibling { z-index: 20; }

Even with 9999:

sibling (20) sits above parent (10) → child trapped.

Key rule:

z-index comparisons only work inside same stacking context.

---

#### Other properties that create stacking contexts (awareness)

- opacity < 1
- transform
- filter

But focus on position + z-index first.

---

### 9. Real-World Patterns

---

#### 9.1 Perfect Centering (Classic Trick)

    .modal {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

True centering.

---

#### 9.2 Floating Button

    .fab {
      position: fixed;
      bottom: 20px;
      right: 20px;
    }

---

#### 9.3 Sticky Section Header

    .section-title {
      position: sticky;
      top: 0;
      background: white;
      z-index: 10;
    }

---

### 10. Common Pitfalls

Sticky not working → missing top or container issues

Absolute jumping unexpectedly → missing positioned parent

z-index “not working” → stacking context problem

Fixed header hiding content → forgot padding/margin compensation

---

### Final Mental Model

static → normal flow only  
relative → normal flow + visual shift + anchor for children  
absolute → removed from flow + positioned to ancestor  
fixed → absolute + viewport anchored  
sticky → relative → fixed on scroll  

Offsets → depend on positioning mode  
z-index → layering within stacking context  
Stacking context → layer groups, not just numbers
