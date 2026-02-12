## Typography in CSS 

### 0. Big Picture – What is Typography?

Typography simply means:

“How text looks on your page.”

When you write HTML:

    <p>Hello world</p>

By default, the browser decides:

- Which font to use
- How big text is
- How bold it is
- How much space between lines

CSS gives you control over all of this.

Think:

Typography = Styling text

---

### 1. font-family – Which font should be used?

This property tells the browser:

“Use this font style for the text.”

Example:

    body {
      font-family: Arial, sans-serif;
    }

Now the browser uses Arial.

---

#### 1.1 How font-family actually works

You almost always provide a list:

    font-family: "Poppins", "Segoe UI", system-ui, sans-serif;

Browser reads LEFT → RIGHT:

1. Try "Poppins"
2. If unavailable → try "Segoe UI"
3. If unavailable → try system-ui
4. Finally → generic sans-serif

Always end with a generic family:

- serif → Times New Roman style (with small feet)
- sans-serif → Clean fonts (Arial, Helvetica)
- monospace → Code fonts (equal width letters)
- cursive / fantasy → Decorative

---

#### 1.2 Common Real-World Pattern

Most modern sites:

    body {
      font-family: system-ui, -apple-system,
                   "Segoe UI", sans-serif;
    }

Why?

Each operating system uses its best default font.

---

#### 1.3 Fonts for Code

    code {
      font-family: "Fira Code", "Consolas",
                   "Courier New", monospace;
    }

---

### 2. font-size – How big is the text?

Controls character size.

Example:

    p {
      font-size: 16px;
    }

---

#### 2.1 Units You’ll Mostly Use

px → Fixed size  
rem → Relative to root (html)  
em → Relative to element  

---

#### 2.2 Best Practice Setup

    html {
      font-size: 16px;
    }

    body {
      font-size: 1rem;
    }

    p {
      font-size: 1rem;
    }

    small {
      font-size: 0.875rem;
    }

    h1 { font-size: 2.5rem; }
    h2 { font-size: 2rem; }
    h3 { font-size: 1.5rem; }

---

#### Why rem?

If html font-size changes → everything scales.

Better for accessibility.

px is fine for tiny UI details.

---

### 3. font-weight – How bold is text?

Controls thickness.

Examples:

    p {
      font-weight: 400;
    }

    strong {
      font-weight: 700;
    }

    h1 {
      font-weight: 600;
    }

---

#### Numeric Scale

100 → Very thin  
400 → Normal  
700 → Bold  
900 → Very heavy  

Important:

Use only weights your font supports.

---

### 4. line-height – Space between lines

Controls vertical breathing room.

Example:

    p {
      line-height: 1.5;
    }

---

#### 4.1 Unitless (Recommended)

    line-height: 1.5;

Means:

line-height = font-size × 1.5

If font-size = 16px:

16 × 1.5 = 24px

---

#### Good Values

Body text → 1.4 – 1.7  
Headings → 1.1 – 1.3  

---

### 5. letter-spacing – Space between letters

Example:

    h1 {
      letter-spacing: 0.05em;
    }

Common use:

Uppercase headings  
Logos  
Buttons  

Avoid large spacing for paragraphs.

---

### 6. word-spacing – Space between words

Example:

    p {
      word-spacing: 0.1em;
    }

Less common but useful sometimes.

---

### 7. text-transform – Change case visually

Values:

none  
uppercase  
lowercase  
capitalize  

Example:

    nav a {
      text-transform: uppercase;
    }

Note:

Purely visual — HTML text stays unchanged.

---

### 8. text-align – Horizontal alignment

Values:

left  
right  
center  
justify  

Examples:

    p {
      text-align: left;
    }

    h1 {
      text-align: center;
    }

justify spreads words across width.

---

### 9. text-decoration – Underlines & lines

Common values:

none  
underline  
line-through  
overline  

Example:

    a {
      text-decoration: none;
    }

    a:hover {
      text-decoration: underline;
    }

---

#### Fine Control (Modern CSS)

    a {
      text-decoration: underline;
      text-decoration-color: blue;
      text-decoration-thickness: 2px;
    }

---

### 10. Web Fonts (Google Fonts)

By default → only system fonts.

Web fonts → load custom fonts.

---

#### 10.1 Add Font Link in HTML

    <link rel="stylesheet"
          href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap">

Place inside `<head>`.

---

#### 10.2 Use in CSS

    body {
      font-family: "Poppins", system-ui, sans-serif;
    }

---

#### 10.3 display=swap

Shows fallback first → swaps later.

Avoids invisible text flashes.

---

#### 10.4 Performance Tip

Avoid loading too many fonts & weights.

Good setup:

1 font family  
2–3 weights  

---

### 11. Practical Typography Base (Real-World Ready)

    html {
      font-size: 16px;
    }

    body {
      font-family: system-ui, -apple-system,
                   "Segoe UI", sans-serif;
      font-size: 1rem;
      line-height: 1.5;
      color: #333;
    }

    h1, h2, h3, h4, h5, h6 {
      font-weight: 600;
      line-height: 1.2;
      margin-bottom: 0.5em;
    }

    h1 { font-size: 2.5rem; }
    h2 { font-size: 2rem; }
    h3 { font-size: 1.5rem; }

    p {
      margin-bottom: 1rem;
    }

    a {
      color: #1f8ef1;
      text-decoration: none;
    }

    a:hover {
      text-decoration: underline;
    }

    nav a {
      text-transform: uppercase;
      letter-spacing: 0.08em;
      font-size: 0.875rem;
    }

    button {
      font-family: inherit;
      font-size: 0.95rem;
      letter-spacing: 0.03em;
    }

---

### 12. Final Cheat-Sheet

font-family → Which font(s)  
font-size → How big  
font-weight → Thickness  
line-height → Space between lines  
letter-spacing → Space between letters  
word-spacing → Space between words  
text-transform → Case control  
text-align → Alignment  
text-decoration → Underlines/lines  

Web fonts:
- Add link in HTML
- Use font-family in CSS
- Don’t overload fonts
