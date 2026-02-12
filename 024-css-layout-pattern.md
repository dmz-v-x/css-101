## Common CSS Layout Patterns  

## 1. Holy Grail Layout

## 1.1 What Is the Holy Grail Layout?

Classic web page structure:

Header at the top  
Footer at the bottom  
Main content in the middle  
Sidebars on left / right  

Rules:

Header & footer span full width  
Content area is flexible  
Sidebars often fixed width  
Layout must adapt on mobile  

Visual mental picture:

Header  
[ Sidebar | Content | Sidebar ]  
Footer  

---

## 1.2 HTML Structure

    <div class="layout">
      <header class="layout-header">Header</header>

      <div class="layout-main">
        <aside class="sidebar left">Left Sidebar</aside>
        <main class="content">Main Content</main>
        <aside class="sidebar right">Right Sidebar</aside>
      </div>

      <footer class="layout-footer">Footer</footer>
    </div>

---

## 1.3 Holy Grail Using Flexbox

### Core Idea

Outer layout → vertical stacking  
Middle section → horizontal layout  

CSS

    html, body {
      height: 100%;
      margin: 0;
    }

    .layout {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }

    .layout-header,
    .layout-footer {
      padding: 1rem;
      background: #1f8ef1;
      color: white;
    }

    .layout-main {
      flex: 1;
      display: flex;
    }

    .sidebar {
      flex: 0 0 200px;
      padding: 1rem;
      background: #f3f4f6;
    }

    .content {
      flex: 1;
      padding: 1rem;
      background: white;
    }

---

### Why This Works

.layout → column flex container  

Stacks:

Header  
Main  
Footer  

.layout-main → row flex container  

Aligns:

Left Sidebar (fixed 200px)  
Content (flexible)  
Right Sidebar (fixed 200px)  

flex: 0 0 200px → fixed width  
flex: 1 → take remaining space  

---

## 1.4 Responsive Holy Grail (Mobile)

CSS

    @media (max-width: 768px) {
      .layout-main {
        flex-direction: column;
      }

      .sidebar {
        flex: 0 0 auto;
        width: 100%;
      }
    }

Now:

Everything stacks vertically on small screens.

---

## 1.5 Holy Grail Using Grid

Grid makes this layout extremely clean.

CSS

    .layout {
      min-height: 100vh;
      display: grid;

      grid-template-columns: 200px 1fr 200px;
      grid-template-rows: auto 1fr auto;

      grid-template-areas:
        "header header header"
        "sidebar-left content sidebar-right"
        "footer footer footer";
    }

    .layout-header  { grid-area: header; }
    .layout-footer  { grid-area: footer; }
    .sidebar.left   { grid-area: sidebar-left; }
    .sidebar.right  { grid-area: sidebar-right; }
    .content        { grid-area: content; }

---

## 1.6 Responsive Grid Version

    @media (max-width: 768px) {
      .layout {
        grid-template-columns: 1fr;
        grid-template-areas:
          "header"
          "sidebar-left"
          "content"
          "sidebar-right"
          "footer";
      }
    }

Grid advantage:

You can literally **see the layout** in grid-template-areas.

---

## 2. Card-Based UI

## 2.1 What Is a Card UI?

Cards = rectangular containers grouping content.

Used everywhere:

Dashboards  
Product listings  
Blog previews  
Galleries  

---

## 2.2 Card HTML

    <section class="card-grid">
      <article class="card">
        <img src="https://picsum.photos/400/200">
        <div class="card-body">
          <h3>Card Title</h3>
          <p>Short description text.</p>
          <button>View</button>
        </div>
      </article>

      <article class="card">
        <img src="https://picsum.photos/401/200">
        <div class="card-body">
          <h3>Another Card</h3>
          <p>More description text.</p>
          <button>View</button>
        </div>
      </article>
    </section>

---

## 2.3 Card Grid Using CSS Grid (Magic Pattern)

CSS

    .card-grid {
      display: grid;
      gap: 1rem;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      padding: 1rem;
    }

---

### Why This Pattern Is Gold

minmax(220px, 1fr)

Card never smaller than 220px  
Card stretches when space available  

auto-fit

Automatically adjusts column count.

✔ No media queries needed.

---

## 2.4 Card Styling

CSS

    .card {
      background: white;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 4px 10px rgba(0,0,0,0.06);
      display: flex;
      flex-direction: column;
      transition: transform 0.2s ease;
    }

    .card:hover {
      transform: translateY(-4px);
    }

    .card img {
      width: 100%;
      height: 160px;
      object-fit: cover;
    }

    .card-body {
      padding: 1rem;
    }

---

## 3. Sidebar Layouts

## 3.1 Basic Sidebar + Content Layout

HTML

    <div class="app-layout">
      <aside class="app-sidebar">Sidebar</aside>
      <main class="app-content">Main Content</main>
    </div>

---

## 3.2 Flexbox Version

CSS

    .app-layout {
      min-height: 100vh;
      display: flex;
    }

    .app-sidebar {
      flex: 0 0 240px;
      background: #111827;
      color: white;
      padding: 1rem;
    }

    .app-content {
      flex: 1;
      padding: 1.5rem;
      background: #f3f4f6;
    }

---

## 3.3 Sticky Sidebar

CSS

    .app-sidebar {
      position: sticky;
      top: 0;
      height: max-content;
    }

Sticky = scrolls with page until reaching top → then sticks.

---

## 4. Sticky Headers

## 4.1 Fixed Header

HTML

    <header class="site-header">Header</header>
    <main>Main Content</main>

CSS

    .site-header {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      height: 60px;
      background: white;
      border-bottom: 1px solid #ddd;
    }

    body {
      margin: 0;
      padding-top: 60px;
    }

---

## 4.2 Sticky Header

CSS

    .section-header {
      position: sticky;
      top: 0;
      background: white;
    }

Sticky behaves like relative → becomes fixed when scrolled.

---

## 5. Split Screen Design

## 5.1 Idea

Two major regions side-by-side.

Used for:

Login pages  
Hero sections  
Comparisons  

---

## 5.2 HTML

    <section class="split-screen">
      <div class="split-left">
        <h1>Welcome</h1>
      </div>
      <div class="split-right">
        <img src="https://picsum.photos/800/600">
      </div>
    </section>

---

## 5.3 Flexbox Version

CSS

    .split-screen {
      min-height: 100vh;
      display: flex;
    }

    .split-left,
    .split-right {
      flex: 1;
    }

    .split-right img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

---

## 5.4 Responsive Split Screen

CSS

    @media (max-width: 768px) {
      .split-screen {
        flex-direction: column;
      }

      .split-right img {
        height: 240px;
      }
    }

---

## Final Mental Model (VERY IMPORTANT)

Every layout = boxes inside boxes.

Step 1 → Identify regions  
Step 2 → Flex or Grid?  

Flex = one direction layouts  
Grid = rows + columns layouts  

Step 3 → Size children:

flex: 1 → flexible  
flex: 0 0 Xpx → fixed  

minmax() → responsive magic  

Step 4 → Add responsiveness:

Change flex-direction  
Change grid-template-columns  

Step 5 → Polish:

Padding  
Background  
Border radius  
Shadow  
Transitions  
