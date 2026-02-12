## Flexbox in CSS 

## 1. Flex Container vs Flex Items

Flexbox starts when you create a **flex container**.

    .container {
      display: flex;
    }

The element with:

    display: flex;

becomes the **flex container**.

Its **direct children** automatically become **flex items**.

Example:

    <div class="container">
      <div class="item">One</div>
      <div class="item">Two</div>
      <div class="item">Three</div>
    </div>

    .container {
      display: flex;
    }

Important rule:

Flexbox only affects **direct children**, not grandchildren.

---

### Two categories of Flexbox properties

**On the container** → control layout behavior

- Direction
- Wrapping
- Alignment
- Spacing

**On the items** → control sizing behavior

- Growth
- Shrinking
- Base size
- Order

---

## 2. Main Axis vs Cross Axis (SUPER IMPORTANT)

Flexbox always works using two invisible directions:

**Main Axis** → where items flow  
**Cross Axis** → perpendicular direction

By default:

    flex-direction: row;

Main axis → Horizontal (left → right)  
Cross axis → Vertical (top ↕ bottom)

If you switch:

    flex-direction: column;

Main axis → Vertical  
Cross axis → Horizontal

---

### Why this matters

Because alignment properties depend on axes:

**justify-content** → aligns along MAIN axis  
**align-items** → aligns along CROSS axis

Always ask:

**“What is my main axis?”**

---

## 3. flex-direction – Choose Row or Column

    .container {
      display: flex;
      flex-direction: row;
    }

Values:

- row (default)
- row-reverse
- column
- column-reverse

Example:

    .row-layout {
      display: flex;
      flex-direction: row;
    }

    .column-layout {
      display: flex;
      flex-direction: column;
    }

Use **row** for:

- Navbars
- Horizontal menus
- Card rows

Use **column** for:

- Vertical layouts
- Sidebars
- Full-height sections

---

## 4. justify-content – Main Axis Alignment

Controls spacing along **main axis**.

    .container {
      display: flex;
      justify-content: center;
    }

Common values:

- flex-start (default)
- flex-end
- center
- space-between
- space-around
- space-evenly

---

### Visual intuition

**space-between**

First item → start  
Last item → end  
Others → evenly spaced

Example:

    .nav {
      display: flex;
      justify-content: space-between;
    }

Perfect for navbars.

---

## 5. align-items – Cross Axis Alignment

Controls alignment along **cross axis**.

    .container {
      display: flex;
      align-items: center;
    }

Values:

- stretch (default)
- flex-start
- flex-end
- center
- baseline

---

### Example – Vertical centering in row

    .header {
      display: flex;
      align-items: center;
    }

Logo + links align beautifully.

---

## 6. align-content – Multi-line Alignment

This property is often misunderstood.

It works ONLY when:

- Items wrap
- Multiple rows exist
- Extra space exists on cross axis

    .container {
      display: flex;
      flex-wrap: wrap;
      align-content: center;
    }

It aligns **entire rows**, not items.

If there’s only one row → no visible effect.

---

## 7. flex-wrap – Allow Next Line

Default behavior:

    flex-wrap: nowrap;

Items stay on one line.

Values:

- nowrap (default)
- wrap
- wrap-reverse

Example:

    .cards {
      display: flex;
      flex-wrap: wrap;
    }

Items move to next row when needed.

---

## 8. Flex Item Sizing DNA

Three core properties:

- flex-grow
- flex-shrink
- flex-basis

Usually written via shorthand:

    flex: grow shrink basis;

---

### 8.1 flex-basis – Starting Size

Preferred size along main axis.

    .item {
      flex-basis: 200px;
    }

Row → basis = width  
Column → basis = height

---

### 8.2 flex-grow – Share Extra Space

    .item {
      flex-grow: 1;
    }

Higher number → larger share.

Example:

    .item1 { flex-grow: 1; }
    .item2 { flex-grow: 2; }

item2 grows twice as much.

---

### 8.3 flex-shrink – Handle Tight Space

    .item {
      flex-shrink: 1;
    }

Higher number → shrinks more.

Set:

    flex-shrink: 0;

to prevent shrinking (use carefully).

---

## 8.4 flex – The Shorthand You’ll Use Most

    .item {
      flex: 1;
    }

Equivalent:

    flex: 1 1 0;

Very common patterns:

    .equal {
      flex: 1;
    }

    .card {
      flex: 1 1 250px;
    }

Meaning:

Grow → yes  
Shrink → yes  
Base size → 250px

---

## 9. Other Useful Flexbox Properties

---

### 9.1 gap – Spacing Without Margin Hacks

    .container {
      display: flex;
      gap: 16px;
    }

Clean & modern.

---

### 9.2 align-self – Override Single Item Alignment

    .item.special {
      align-self: flex-start;
    }

Values same as align-items.

---

### 9.3 order – Change Visual Order

    .featured {
      order: -1;
    }

Be careful → DOM order unchanged.

---

### 9.4 flex-flow – Shorthand

    .container {
      flex-flow: row wrap;
    }

Equivalent:

flex-direction + flex-wrap

---

## 10. Real-World Layout Patterns

---

## 10.1 Navbar (Classic Layout)

    <header class="navbar">
      <div class="logo">MySite</div>
      <nav class="nav-links">
        <a href="#">Home</a>
        <a href="#">Docs</a>
        <a href="#">About</a>
      </nav>
    </header>

    .navbar {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .nav-links {
      display: flex;
      gap: 1rem;
    }

---

## 10.2 Perfect Centering (Flexbox’s Killer Feature)

    .center {
      display: flex;
      justify-content: center;
      align-items: center;
    }

Full screen:

    .full-center {
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
    }

---

## 10.3 Responsive Card Rows

    .cards {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
    }

    .card {
      flex: 1 1 250px;
    }

Large screen → many per row  
Small screen → wrap automatically

---

## 10.4 Sidebar + Content

    .layout {
      display: flex;
    }

    .sidebar {
      flex: 0 0 250px;
    }

    .content {
      flex: 1;
    }

---

## 10.5 Equal Button Groups

    .button-row {
      display: flex;
      gap: 0.5rem;
    }

    .button-row button {
      flex: 1;
    }

---

## 10.6 Push Item to End (Common Trick)

    .push-right {
      margin-left: auto;
    }

Works beautifully in flex layouts.

---

## 11. Core Concepts You Must Remember

Flexbox = 1D layout system.

Main mental model:

flex-direction → defines main axis  
justify-content → main axis alignment  
align-items → cross axis alignment  

Container controls layout  
Items control sizing  

Most used item shorthand:

    flex: grow shrink basis;

Most common patterns:

    flex: 1;
    flex: 1 1 250px;

Most common container helpers:

    display: flex;
    gap: ...
    flex-wrap: wrap;
