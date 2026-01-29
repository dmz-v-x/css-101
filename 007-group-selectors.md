## Group Selectors

### 1. What are group selectors

A **group selector** lets you apply the same CSS styles to **many different selectors at once**.

Instead of writing the same styles again and again, you write them once and separate selectors using a comma `,`.

Example:

    h1, h2, h3 {
      font-family: Arial, sans-serif;
      color: #333;
    }

This is just a shorter way of writing:

    h1 { font-family: Arial, sans-serif; color: #333; }
    h2 { font-family: Arial, sans-serif; color: #333; }
    h3 { font-family: Arial, sans-serif; color: #333; }

So the idea is simple:
- Same styles
- Multiple selectors
- Less repetition

---

### 2. Basic syntax rules you must understand

#### 2.1. Comma means “OR”, not “AND”

When you write:

    h1, h2, h3 { ... }

It means:
- h1 **OR**
- h2 **OR**
- h3

Any element that matches **any one** of these selectors gets the styles.

Each selector stands alone.

---

#### 2.2. Spaces around commas don’t matter

All of these work exactly the same:

    h1,h2,h3 { ... }
    h1, h2, h3 { ... }
    h1 ,h2 , h3 { ... }

Spaces are only for readability.
Use spaces to make your CSS easier to read.

---

#### 2.3. Each comma-separated part must be a complete selector

This is valid:

    p,
    .highlight,
    #typography {
      margin-bottom: 16px;
    }

Because:
- `p` is a valid selector
- `.highlight` is a valid selector
- `#typography` is a valid selector

Each part works on its own.

---

This is a very common beginner mistake:

    .card, .box p {
      color: red;
    }

What this actually means:
- `.card` → any element with class card
- `.box p` → any paragraph inside .box

If you **intended**:
“paragraphs inside .card OR inside .box”

You must write:

    .card p,
    .box p {
      color: red;
    }

Rule to remember:
**Every chunk between commas must be a full selector by itself.**

---

#### 2.4. You can mix selector types in one group

You can mix element, class, id, and combined selectors:

    h1,
    .highlight,
    #header-title,
    nav a {
      text-transform: uppercase;
    }

This targets:
- all h1 elements
- any element with class highlight
- the element with id header-title
- all links inside nav

All of them get the same styles.

---

### 3. How browsers treat group selectors

#### 3.1. Browser treats it like many separate rules

When the browser sees:

    h1, h2, h3 {
      color: red;
    }

Internally, it behaves like:

    h1 { color: red; }
    h2 { color: red; }
    h3 { color: red; }

They just share the same style block.

---

#### 3.2. Strength is calculated per selector, not per group

This is very important.

This group:

    p,
    .highlight,
    #msg {
      color: red;
    }

Does **not** have one single strength.

Instead:
- `p` keeps element-level strength
- `.highlight` keeps class-level strength
- `#msg` keeps id-level strength

They are never averaged or merged.

If an element matches more than one of them, normal override rules apply.

---

#### 3.3. Order still matters

Even though there are many selectors, this is still **one rule block** in the file.

So if later you write:

    .highlight {
      color: blue;
    }

That later rule can override the earlier grouped rule for `.highlight`.

---

### 4. Why group selectors are useful in real projects

#### 4.1. Avoid repeating yourself

Instead of:

    h1 { font-family: system-ui; }
    h2 { font-family: system-ui; }
    h3 { font-family: system-ui; }

You write:

    h1, h2, h3 {
      font-family: system-ui;
    }

Cleaner and easier to change later.

---

#### 4.2. Keep design consistent

Grouping makes you think in **design groups**.

For example:
“All headings should feel related.”

Group selectors naturally enforce consistency.

---

#### 4.3. Smaller and cleaner CSS

Less repetition:
- Easier to read
- Easier to maintain
- Fewer chances for mistakes

---


### 5. Common mistakes beginners make

#### Mistake 1: Forgetting commas

Wrong:

    .card .box .alert {
      color: red;
    }

This means:
.alert inside .box inside .card

Correct grouping:

    .card,
    .box,
    .alert {
      color: red;
    }

---

#### Mistake 2: Incomplete selectors

Always check:
Does each comma-separated part make sense on its own?

---

#### Mistake 3: Grouping unrelated things

Avoid this:

    h1, p, button, input, table, a {
      color: blue;
    }

Grouping should reflect **design intent**, not just saving lines.

