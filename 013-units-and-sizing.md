## Units and sizing

### 1. Absolute units

### 1.1 px – CSS pixels

px means CSS pixel.  
It is not always exactly one physical screen pixel, but you can think of it as a fixed step.

Example:

    .box {
      width: 200px;
      height: 100px;
    }

No matter the screen size, this box stays 200px wide and 100px tall.

Good things about px:
- Simple and predictable
- Great for borders, icons, shadows, and small precise adjustments

Not so good:
- If everything uses px, text may not scale well for accessibility or different devices

Rule of thumb:
Use px for precise visual details.
Prefer relative units for text and layout.

### 1.2 cm, mm, in, pt

These are physical units:
- cm = centimeters
- mm = millimeters
- in = inches
- pt = points (1/72 inch)

Example:

    .card {
      width: 5cm;
    }

These units make the most sense for print styles.

On screens:
- They are approximations
- Different devices treat them differently

For normal websites, you will almost never use these.
Stick to px and relative units.

---

### 2. Relative units – they depend on something

Relative units scale based on:
- parent size
- root font size
- viewport size

These are the most important ones.

### 2.1 Percentage %

Percent means “a part of something else”.
What it refers to depends on the property.

### 2.1.1 Width and height

Width percentages are relative to the parent’s width.

Example:

    .container {
      width: 800px;
    }

    .box {
      width: 50%;
    }

If .box is inside .container:
- 50% of 800px = 400px

Height percentages are relative to the parent’s height,
but only if the parent has an explicit height.
If the parent’s height is auto, percentages may not work as expected.

### 2.1.2 Margin and padding in %

Horizontal percentages are usually based on parent width.

Example:

    margin-left: 10%;

If parent width is 1000px:
- 10% = 100px

### 2.1.3 Font-size in %

Font-size percentages are relative to the parent’s font-size.

Example:

    .parent {
      font-size: 20px;
    }

    .child {
      font-size: 150%;
    }

Child font-size:
- 150% of 20px = 30px

---

### 2.2 em – relative to the current element’s font size

1em equals the font-size of the element itself.

If no font-size is set, it uses the inherited size.

### 2.2.1 em for font-size

Example:

    body {
      font-size: 16px;
    }

    p {
      font-size: 1.5em;
    }

1.5em × 16px = 24px

If nested:

    .container {
      font-size: 20px;
    }

    .container p {
      font-size: 1.5em;
    }

Now:
- 1em = 20px
- 1.5em = 30px

### 2.2.2 em for spacing

em is useful when spacing should scale with text.

Example:

    p {
      font-size: 16px;
      margin-bottom: 1.5em;
    }

Margin-bottom becomes 24px.
If text grows, spacing grows too.

### 2.2.3 em compounding

em compounds when nested.

Example:

    .container {
      font-size: 1.25em;
    }

    .container p {
      font-size: 1.25em;
    }

If body is 16px:
- container = 20px
- paragraph = 25px

This can cause unexpectedly large text if overused.

---

### 2.3 rem – relative to the root element

rem means root em.
It is always relative to the html element.

Default browser setting:

    html {
      font-size: 16px;
    }

So:
- 1rem = 16px
- 2rem = 32px

Example:

    h1 {
      font-size: 2.5rem;
    }

    p {
      font-size: 1rem;
    }

    small {
      font-size: 0.875rem;
    }

Big advantage of rem:
- predictable
- respects user font-size settings
- does not compound with nesting

This makes rem ideal for typography and global spacing.

---

### 2.4 Viewport units – vw, vh, vmin, vmax

Viewport means the visible browser window.

- 1vw = 1% of viewport width
- 1vh = 1% of viewport height
- 1vmin = smaller of width/height
- 1vmax = larger of width/height

Example:
If viewport width is 1200px:
- 1vw = 12px
- 50vw = 600px

### 2.4.1 Common uses

Full-height sections:

    .hero {
      height: 100vh;
    }

Text that scales with screen width:

    h1 {
      font-size: 5vw;
    }

Often combined with clamp:

    h1 {
      font-size: clamp(1.5rem, 4vw, 3rem);
    }

Meaning:
- minimum size
- flexible middle
- maximum size

vmin and vmax example:

    .circle {
      width: 20vmin;
      height: 20vmin;
      border-radius: 50%;
    }

This keeps the circle fitting inside the viewport.

---

### 3. When to use each unit

### 3.1 Font sizes

Best choice: rem

Example:

    h1 { font-size: 2.5rem; }
    p  { font-size: 1rem; }
    small { font-size: 0.875rem; }

Use em when spacing should scale with text:

    button {
      font-size: 1rem;
      padding: 0.5em 1em;
    }

Avoid px for font sizes in large layouts unless absolutely necessary.

---

### 3.2 Spacing (margin, padding, gap)

Good choices:
- rem for consistent rhythm
- em for component-based scaling
- % or vw for fluid layouts

Example spacing scale:

    :root {
      --space-sm: 0.5rem;
      --space-md: 1rem;
      --space-lg: 1.5rem;
    }

    .card {
      padding: var(--space-md);
      margin-bottom: var(--space-lg);
    }

---

### 3.3 Widths and heights

Common patterns:

- % for flexible layouts
- px or rem for fixed components
- vw/vh for full-screen sections

Examples:

    .col {
      width: 50%;
    }

    .sidebar {
      width: 250px;
    }

    .hero {
      min-height: 100vh;
    }

---

### 3.4 Borders and shadows

Use px for crisp visuals:

    .card {
      border: 1px solid #ddd;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

---

### 4. Putting it all together

Example card style:

    *,
    *::before,
    *::after {
      box-sizing: border-box;
    }

    .card {
      width: min(90vw, 20rem);
      padding: 1.5rem;
      margin: 1rem auto;
      border-radius: 0.5rem;
      border: 1px solid #ddd;
      font-size: 1rem;
    }

Used units:
- vw for responsiveness
- rem for spacing and typography
- px for borders

This combination gives predictable, accessible, and flexible layouts.
