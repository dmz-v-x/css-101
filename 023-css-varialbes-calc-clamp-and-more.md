## CSS Variables, calc(), clamp(), object-fit, filter & More  

## 1. CSS Variables (Custom Properties)

## 1.1 What They Are

CSS variables are reusable values.

Instead of repeating colors, spacing, sizes everywhere:

You define once → reuse many times.

They start with `--`

Example variable names:

--primary  
--text-color  
--space-md  

You read them using `var()`.

---

## 1.2 Basic Example – Reusable Colors

HTML

    <div class="card">
      <h2>Card Title</h2>
      <p>This is a simple card.</p>
      <button>Click Me</button>
    </div>

CSS

    :root {
      --primary: #1f8ef1;
      --card-bg: #ffffff;
      --text-main: #222;
    }

    body {
      background: #f5f7fb;
      font-family: sans-serif;
    }

    .card {
      background: var(--card-bg);
      color: var(--text-main);
      padding: 20px;
      width: 280px;
      margin: 40px auto;
      border-radius: 10px;
    }

    button {
      background: var(--primary);
      color: white;
      border: none;
      padding: 10px 14px;
      border-radius: 6px;
      cursor: pointer;
    }

Now change:

    --primary: red;

EVERY button updates automatically.

---

## 1.3 Overriding Variables (Super Important)

Variables follow normal CSS rules.

Closest definition wins.

HTML

    <div class="card">
      <button>Normal Button</button>
    </div>

    <div class="card danger">
      <button>Danger Button</button>
    </div>

CSS

    :root {
      --primary: #1f8ef1;
    }

    .danger {
      --primary: #e74c3c;
    }

    button {
      background: var(--primary);
      color: white;
      border: none;
      padding: 10px 14px;
    }

Result:

Normal card → blue button  
Danger card → red button  

Same CSS rule, different variable values.

---

## 1.4 Fallback Values

If variable is missing → use default.

CSS

    p {
      color: var(--text-main, #333);
    }

If `--text-main` exists → use it  
Else → use #333

---

## 1.5 Dark / Light Theme Example

HTML

    <body class="dark">
      <div class="card">
        <h2>Dark Mode</h2>
        <button>Button</button>
      </div>
    </body>

CSS

    :root {
      --bg: white;
      --text: #111;
      --primary: #1f8ef1;
    }

    body.dark {
      --bg: #0d1117;
      --text: #e6edf3;
      --primary: #58a6ff;
    }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: sans-serif;
    }

    button {
      background: var(--primary);
      color: white;
    }

Toggle class → entire theme changes.

---

# 2. calc() – Math Inside CSS

## 2.1 What calc() Does

Allows calculations using mixed units.

Example:

    width: calc(100% - 20px);

Meaning:

Full width minus 20px.

---

## 2.2 Example – Layout With Padding Math

HTML

    <div class="container">
      <div class="box">Content</div>
    </div>

CSS

    .container {
      width: 400px;
      padding: 20px;
      border: 2px solid black;
      margin: 40px auto;
    }

    .box {
      width: calc(100% - 40px);
      background: #1f8ef1;
      color: white;
      padding: 10px;
    }

Why 40px?

Padding left + right = 20 + 20.

---

## 2.3 Example – Full Height Minus Header

HTML

    <header>Header</header>
    <main>Main Content</main>

CSS

    header {
      height: 60px;
      background: black;
      color: white;
    }

    main {
      height: calc(100vh - 60px);
      background: #eee;
    }

Viewport height minus header height.

---

## 2.4 Syntax Gotcha (CRITICAL)

Correct:

    calc(100% - 20px)

Wrong:

    calc(100%-20px)

Spaces matter.

---

# 3. clamp() – Smart Min / Preferred / Max

## 3.1 What clamp() Does

clamp(min, preferred, max)

Use preferred value, but:

Never smaller than min  
Never larger than max  

---

## 3.2 Example – Fluid Typography

HTML

    <h1>Responsive Heading</h1>

CSS

    h1 {
      font-size: clamp(1.5rem, 5vw, 3rem);
    }

Small screens → 1.5rem  
Medium → scales with vw  
Huge → capped at 3rem

---

## 3.3 Example – Responsive Card Width

HTML

    <div class="card">Card</div>

CSS

    .card {
      width: clamp(220px, 40vw, 360px);
      background: #1f8ef1;
      color: white;
      padding: 20px;
      margin: 40px auto;
    }

Never too tiny  
Never too wide

---

# 4. object-fit & object-position

Used for images inside fixed boxes.

---

## 4.1 Example – Thumbnail Crop

HTML

    <div class="thumb">
      <img src="https://picsum.photos/400/300">
    </div>

CSS

    .thumb {
      width: 260px;
      height: 160px;
      overflow: hidden;
      border-radius: 10px;
      margin: 40px auto;
    }

    .thumb img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

cover = fill box, crop edges.

---

## 4.2 contain Example

CSS

    object-fit: contain;

Entire image visible, may leave gaps.

---

## 4.3 object-position Example

CSS

    object-fit: cover;
    object-position: top;

Focus top part of image.

---

# 5. filter – Visual Effects

Applies effects like blur, brightness, grayscale.

---

## 5.1 Blur Example

HTML

    <img class="demo-img" src="https://picsum.photos/300/200">

CSS

    .demo-img {
      display: block;
      margin: 40px auto;
      filter: blur(3px);
    }

---

## 5.2 Brightness Hover Effect

HTML

    <div class="card">
      <img src="https://picsum.photos/300/200">
    </div>

CSS

    .card img {
      width: 100%;
      transition: filter 0.3s ease;
      filter: brightness(0.8);
    }

    .card:hover img {
      filter: brightness(1.1);
    }

---

## 5.3 Grayscale Hover

CSS

    filter: grayscale(1);

Hover → grayscale(0)

---

# 6. backdrop-filter – Glass Effect

Blurs WHAT’S BEHIND element.

---

## 6.1 Glass Card Example

HTML

    <div class="glass-card">
      <h2>Glass UI</h2>
    </div>

CSS

    body {
      background: linear-gradient(135deg, #1f8ef1, #5e72e4);
    }

    .glass-card {
      width: 320px;
      margin: 60px auto;
      padding: 20px;
      border-radius: 12px;

      background: rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);

      color: white;
    }

Needs transparency + background behind.

---

# 7. mix-blend-mode – Photoshop-Like Blending

Blends element with background.

---

## 7.1 Text Blend Example

HTML

    <div class="hero">
      <h1>Blended Text</h1>
    </div>

CSS

    .hero {
      background: linear-gradient(45deg, red, blue);
      padding: 60px;
      text-align: center;
    }

    h1 {
      color: white;
      mix-blend-mode: overlay;
    }

---

## 7.2 Color Overlay Example

HTML

    <div class="image-wrap">
      <img src="https://picsum.photos/400/250">
    </div>

CSS

    .image-wrap {
      position: relative;
      width: 400px;
      margin: 40px auto;
    }

    .image-wrap img {
      width: 100%;
      display: block;
    }

    .image-wrap::after {
      content: "";
      position: absolute;
      inset: 0;
      background: red;
      mix-blend-mode: multiply;
    }

Tinted image effect.

---

# Final Cheat Sheet

CSS Variables → reusable design values  
calc() → math with mixed units  
clamp() → min / fluid / max sizing  
object-fit → control image cropping  
filter → blur, brightness, grayscale etc.  
backdrop-filter → blur background behind element  
mix-blend-mode → blend visuals like image editors
