## CSS Grid

## 1. Grid Container vs Grid Items

Grid starts when you turn an element into a **grid container**.

    .container {
      display: grid;
    }

The element with:

    display: grid;

becomes the **grid container**.

Its **direct children** automatically become **grid items**.

Example:

    <div class="grid-container">
      <div class="item">1</div>
      <div class="item">2</div>
      <div class="item">3</div>
      <div class="item">4</div>
    </div>

    .grid-container {
      display: grid;
    }

Once Grid is activated, you can control:

• Number of columns  
• Number of rows  
• Size of tracks  
• Exact placement of items  

---

## 2. Grid Tracks = Rows + Columns

A grid is made of:

Vertical divisions → **Columns**  
Horizontal divisions → **Rows**

Each row or column is called a **track**.

Visual mental model:

Columns:

| Col 1 | Col 2 | Col 3 |

Rows:

Row 1 → cells across  
Row 2 → cells across  

So Grid is inherently **2D**.

---

## 3. grid-template-columns / grid-template-rows

These properties define your grid structure.

They answer:

“How many tracks?”  
“How big is each track?”

---

### 3.1 Equal Columns (Most Common)

    .grid {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
    }

Meaning:

3 columns  
Each column = equal share of space

Shortcut:

    grid-template-columns: repeat(3, 1fr);

Same result, cleaner syntax.

---

### 3.2 Mixing Fixed + Flexible

    grid-template-columns: 200px 1fr 2fr;

Column 1 → Always 200px  
Remaining space → Split into 3 parts

Column 2 → 1 part  
Column 3 → 2 parts (twice as wide)

---

### 3.3 Rows Work the Same Way

    .grid {
      grid-template-rows: 100px 200px auto;
    }

Row 1 → 100px high  
Row 2 → 200px  
Row 3 → height based on content

If rows are not defined → Grid creates them automatically.

---

## 4. Spacing Between Items – gap

You almost always want spacing.

    .grid {
      display: grid;
      gap: 16px;
    }

gap = space between rows AND columns.

Different values:

    row-gap: 10px;
    column-gap: 20px;

Modern CSS uses simply:

    gap

Older code may show:

    grid-gap

---

## 5. Grid Lines & Item Placement

Grids are defined by **lines**, not just boxes.

For 3 columns → 4 vertical lines:

| 1 | 2 | 3 | 4 |

For 2 rows → 3 horizontal lines.

Items are placed using line numbers.

---

### 5.1 grid-column / grid-row

    .item {
      grid-column: 1 / 3;
      grid-row: 1 / 2;
    }

Meaning:

Start at column line 1  
End at column line 3  
→ spans 2 columns

Row line 1 → line 2  
→ first row only

---

### 5.2 Example – Featured Item

    .featured {
      grid-column: 1 / 3;
    }

Item becomes wider across two columns.

---

### 5.3 grid-area (Numeric Shorthand)

Format:

    grid-area: row-start / column-start / row-end / column-end;

Example:

    .item {
      grid-area: 1 / 1 / 2 / 3;
    }

Equivalent to:

    grid-row: 1 / 2;
    grid-column: 1 / 3;

---

## 6. Explicit vs Implicit Grid

---

### 6.1 Explicit Grid

Tracks you define manually.

    grid-template-columns
    grid-template-rows

Example:

    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: 150px 150px;

Grid = 3 × 2

---

### 6.2 Implicit Grid

Created automatically when needed.

If items exceed defined tracks → Grid adds rows.

By default → auto height.

Control size:

    .grid {
      grid-auto-rows: 200px;
    }

Every new row = 200px high.

---

## 7. The fr Unit – Fractional Space

fr = fraction of remaining space.

Browser:

1. Subtracts fixed sizes  
2. Divides leftover space among fr units  

Example:

    grid-template-columns: 1fr 1fr 2fr;

Total fractions = 4

Space distribution:

Column 1 → 25%  
Column 2 → 25%  
Column 3 → 50%

---

## 8. minmax() – Flexible Tracks

Defines minimum + maximum size.

    grid-template-columns: minmax(200px, 1fr);

Column:

Never smaller than 200px  
Can grow flexibly

Extremely useful for responsiveness.

---

## 9. repeat() – Cleaner Syntax

Instead of:

    1fr 1fr 1fr 1fr

Write:

    repeat(4, 1fr)

Dynamic repetition:

    repeat(auto-fit, ...)

---

## 10. auto-fit vs auto-fill (Responsive Magic)

Most important responsive pattern:

    .grid {
      display: grid;
      gap: 16px;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    }

Let’s decode:

auto-fit → create as many columns as fit  
minmax(250px, 1fr) →

• Minimum width = 250px  
• Flexible growth allowed  

---

### Behavior:

Large screen → many columns  
Small screen → fewer columns  
Very small → single column  

No media queries required.

---

### auto-fill vs auto-fit

auto-fill → keeps empty tracks  
auto-fit → collapses empty tracks

Practical rule:

Use **auto-fit** for responsive cards.

---

## 11. Alignment in Grid

Grid has TWO alignment levels.

---

### 11.1 Inside Each Cell

    justify-items → horizontal alignment  
    align-items   → vertical alignment

Example:

    .grid {
      justify-items: center;
      align-items: center;
    }

Items centered inside cells.

Override per item:

    .item {
      justify-self: end;
      align-self: start;
    }

---

### 11.2 Whole Grid Alignment

Moves the grid itself.

    justify-content  
    align-content

Useful when grid smaller than container.

---

## 12. Named Areas (Beautiful Layout System)

You can visually design layouts.

    .page {
      display: grid;
      grid-template-columns: 200px 1fr;
      grid-template-areas:
        "header header"
        "sidebar main"
        "footer footer";
    }

Assign items:

    .header  { grid-area: header; }
    .sidebar { grid-area: sidebar; }
    .main    { grid-area: main; }
    .footer  { grid-area: footer; }

Readable & powerful.

---

## 13. Real-World Patterns

---

## 13.1 Simple Card Grid

    .cards {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 16px;
    }

---

## 13.2 Fully Responsive Cards (Golden Pattern)

    .cards {
      display: grid;
      gap: 16px;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    }

This pattern alone replaces tons of media queries.

---

## 13.3 Sidebar Layout

    .layout {
      display: grid;
      grid-template-columns: 250px 1fr;
    }

Sidebar fixed  
Content flexible

---

## 13.4 Holy Grail Layout

    .page {
      display: grid;
      grid-template-columns: 220px 1fr;
      grid-template-rows: auto 1fr auto;
      grid-template-areas:
        "header header"
        "sidebar main"
        "footer footer";
    }

---

## 13.5 Perfect Image Gallery

    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      grid-auto-rows: 150px;
      gap: 10px;
    }

    .gallery img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

Uniform grid with cropped images.

---

## 14. What You Must Remember

Grid = 2D layout system.

Turn on grid:

    display: grid;

Define tracks:

    grid-template-columns
    grid-template-rows

Spacing:

    gap

Responsive magic:

    repeat(auto-fit, minmax(...))

Sizing tools:

    fr
    minmax()
    repeat()

Placement tools:

    grid-column
    grid-row
    grid-area

Alignment tools:

    justify-items / align-items
    justify-content / align-content

Named layouts:

    grid-template-areas
