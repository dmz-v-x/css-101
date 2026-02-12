## CSS Transitions

## 1. How CSS Transitions Work (Core Idea)

A transition is NOT a standalone animation.

It needs **four things**:

### ✅ 1. Start State  
Initial CSS values.

### ✅ 2. End State  
New CSS values (hover, focus, class change, etc.)

### ✅ 3. Trigger  
Something that causes the change:

:hover  
:focus  
:active  
Adding/removing class  
JavaScript change  

### ✅ 4. Transition Definition  
Rules telling browser:

👉 WHAT to animate  
👉 HOW LONG  
👉 HOW it moves (speed curve)  
👉 WHEN it starts  

---

### Example

	button {
	  background-color: #1f8ef1;
	  transition: background-color 0.3s ease;
	}

	button:hover {
	  background-color: #0c6cd4;
	}

Flow:

Initial → Blue  
Hover → Darker Blue  
Transition → Smooth color fade (0.3s)

Without transition → instant jump

---

## 2. transition-property – WHAT animates

This tells the browser which property should animate.

---

### Single Property

	.button {
	  transition-property: background-color;
	}

Meaning:

“If background-color changes → animate it”

---

### Multiple Properties

	.button {
	  transition-property: background-color, transform, opacity;
	}

Each listed property animates when changed.

---

### Using `all`

	.button {
	  transition-property: all;
	}

Meaning:

“All animatable properties transition”

⚠️ Convenient but risky.  
Better practice → be explicit.

---

## 3. transition-duration – HOW LONG animation runs

Controls speed.

---

### Examples

	transition-duration: 0.3s;
	transition-duration: 200ms;

Units:

s → seconds  
ms → milliseconds  

---

### Multiple Durations

	transition-property: opacity, transform;
	transition-duration: 200ms, 400ms;

opacity → 200ms  
transform → 400ms

---

## 4. transition-timing-function – SPEED CURVE

Controls motion feel.

---

### Common Values

	ease (default)
	linear
	ease-in
	ease-out
	ease-in-out

---

### Mental Feelings

ease → natural smooth  
linear → robotic constant  
ease-in → slow start  
ease-out → smooth stop (great for hover)  
ease-in-out → smooth both ends

---

### Example

	button {
	  transition: transform 0.2s ease-out;
	}

	button:hover {
	  transform: translateY(-2px);
	}

Hover → smooth lift effect

---

## 5. transition-delay – WAIT BEFORE START

Adds pause before animation.

---

### Example

	.card {
	  opacity: 0;
	  transition: opacity 0.5s ease 0.2s;
	}

	.card.visible {
	  opacity: 1;
	}

Flow:

Opacity changes → wait 0.2s → animate 0.5s

---

## 6. Transition Shorthand (MOST COMMON)

Instead of writing 4 properties:

	property + duration + timing + delay

---

### Syntax

	transition: <property> <duration> <timing> <delay>;

---

### Examples

	transition: background-color 0.3s ease;
	transition: opacity 0.2s linear;
	transition: transform 0.25s ease-out 0.1s;

---

### Multiple Transitions

	transition:
	  transform 0.3s ease,
	  opacity 0.2s linear;

---

## 7. Which Properties Can Animate?

Generally → numeric & interpolatable values.

---

### ✅ Works Well

Colors  
Opacity  
Transform  
Width / Height  
Padding / Margin  
Border-radius  
Box-shadow  

---

### ❌ Cannot Animate Smoothly

display  
position (static → absolute)  
visibility (sometimes abrupt)

---

### Workaround for display

Use:

opacity  
transform  
max-height  

---

## 8. Practical UI Patterns

---

## 8.1 Button Hover (Classic)

	button {
	  background-color: #1f8ef1;
	  transition:
	    background-color 0.25s ease,
	    transform 0.15s ease;
	}

	button:hover {
	  background-color: #0c6cd4;
	  transform: translateY(-2px);
	}

Effect:

Smooth color fade + lift

---

## 8.2 Smooth Underline Links

	a {
	  position: relative;
	  text-decoration: none;
	}

	a::after {
	  content: "";
	  position: absolute;
	  left: 0;
	  bottom: -2px;
	  width: 0;
	  height: 2px;
	  background: currentColor;
	  transition: width 0.2s ease-out;
	}

	a:hover::after {
	  width: 100%;
	}

Underline grows smoothly.

---

## 8.3 Card Hover Lift

	.card {
	  transform: translateY(0);
	  box-shadow: 0 0 0 rgba(0,0,0,0);
	  transition:
	    transform 0.2s ease,
	    box-shadow 0.2s ease;
	}

	.card:hover {
	  transform: translateY(-4px);
	  box-shadow: 0 8px 16px rgba(0,0,0,0.12);
	}

Professional “hover lift”.

---

## 8.4 Fade-In Elements

	.item {
	  opacity: 0;
	  transition: opacity 0.3s ease-out;
	}

	.item.visible {
	  opacity: 1;
	}

---

## 8.5 Fade + Slide Combo (Modern UI Favorite)

	.item {
	  opacity: 0;
	  transform: translateY(8px);
	  transition:
	    opacity 0.3s ease-out,
	    transform 0.3s ease-out;
	}

	.item.visible {
	  opacity: 1;
	  transform: translateY(0);
	}

Smooth entrance animation.

---

## 8.6 Dropdown / Accordion Trick

Height → cannot animate to `auto`

Use max-height.

	.content {
	  max-height: 0;
	  overflow: hidden;
	  transition: max-height 0.3s ease;
	}

	.content.open {
	  max-height: 500px;
	}

---

## 9. Best Placement Rule (IMPORTANT)

Always define transition on **base state**.

---

### ✅ Correct

	.button {
	  transition: background-color 0.3s ease;
	}

	.button:hover {
	  background-color: red;
	}

---

### ❌ Wrong

	.button:hover {
	  transition: background-color 0.3s ease;
	}

Causes one-way weirdness.

---

## 10. Performance Best Practices

---

### ✅ Prefer Animating

opacity  
transform  

Why?

GPU accelerated → smoother.

---

### ⚠️ Use Carefully

width  
height  
top / left  

These trigger layout recalculations.

---

### Good Duration Guidelines

Hover → 0.15s – 0.3s  
Entrance → 0.3s – 0.6s  
Avoid slow UI → feels laggy

---

## 11. Common Pitfalls

---

### ❌ Pitfall 1 – Transitioning Everything

	transition: all 1s;

Too slow & unpredictable.

---

### ❌ Pitfall 2 – Animating Non-Animatable Properties

	display → won’t animate

---

### ❌ Pitfall 3 – Long Durations on Hover

Feels sluggish.

---

## 12. Quick Cheat Sheet

Transitions need:

	Start State  
	End State  
	Trigger  
	Transition Definition  

Core Properties:

	transition-property  
	transition-duration  
	transition-timing-function  
	transition-delay  

Shorthand:

	transition: property duration timing delay;

Golden UI Pattern:

	transition:
	  transform 0.2s ease,
	  opacity 0.2s ease;

Most Reliable Animations:

	transform + opacity
