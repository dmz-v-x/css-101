## CSS Animations

## 1. Transitions vs Animations (SEE the Difference)

### ✅ Transition → Needs a Trigger

HTML:

<button class="transition-btn">Hover Me</button>

CSS:

.transition-btn {
  background: #1f8ef1;
  color: white;
  padding: 12px 18px;
  border: none;
  border-radius: 6px;

  transition: transform 0.3s ease;
}

.transition-btn:hover {
  transform: scale(1.1);
}

Behavior:

Nothing happens initially.  
Hover → animation occurs.

---

### ✅ Animation → Runs Automatically

HTML:

<button class="animation-btn">I Animate</button>

CSS:

@keyframes pulse {
  from { transform: scale(1); }
  to   { transform: scale(1.1); }
}

.animation-btn {
  background: #ff5a5f;
  color: white;
  padding: 12px 18px;
  border: none;
  border-radius: 6px;

  animation: pulse 0.6s ease-in-out infinite alternate;
}

Behavior:

Runs forever. No hover needed.

---

## 2. @keyframes – The Animation Timeline

HTML:

<div class="box"></div>

CSS:

@keyframes moveRight {
  0%   { transform: translateX(0); }
  100% { transform: translateX(200px); }
}

.box {
  width: 80px;
  height: 80px;
  background: #42e695;

  animation: moveRight 1s ease-in-out infinite alternate;
}

Flow:

Start → Left  
End → Right  
Alternate → Back & forth

---

## 3. Core Animation Properties (One by One)

---

## 3.1 animation-name

HTML:

<div class="fade-box"></div>

CSS:

@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

.fade-box {
  width: 80px;
  height: 80px;
  background: #333;

  animation-name: fadeIn;
  animation-duration: 1s;
}

---

## 3.2 animation-duration

HTML:

<div class="slow-box"></div>

CSS:

@keyframes slide {
  from { transform: translateX(0); }
  to   { transform: translateX(300px); }
}

.slow-box {
  width: 60px;
  height: 60px;
  background: orange;

  animation-name: slide;
  animation-duration: 3s;
}

3s → slow movement.

---

## 3.3 animation-timing-function

HTML:

<div class="linear-box"></div>

CSS:

@keyframes spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}

.linear-box {
  width: 60px;
  height: 60px;
  background: purple;

  animation: spin 1s linear infinite;
}

linear → constant speed.

---

## 3.4 animation-delay

HTML:

<div class="delayed-box"></div>

CSS:

.delayed-box {
  width: 60px;
  height: 60px;
  background: red;

  animation: fadeIn 1s ease 1s forwards;
}

1s delay → waits before starting.

---

## 3.5 animation-iteration-count

HTML:

<div class="three-times"></div>

CSS:

.three-times {
  width: 60px;
  height: 60px;
  background: teal;

  animation: pulse 0.4s ease 0s 3 alternate;
}

Runs exactly 3 times.

---

## 3.6 animation-direction

HTML:

<div class="alternate-box"></div>

CSS:

.alternate-box {
  width: 60px;
  height: 60px;
  background: #5e72e4;

  animation: moveRight 1s ease infinite alternate;
}

alternate → forward → backward → repeat.

---

## 3.7 animation-fill-mode

HTML:

<div class="fill-box"></div>

CSS:

.fill-box {
  width: 60px;
  height: 60px;
  background: #42e695;

  animation: moveRight 1s ease forwards;
}

forwards → stays at final state.

Without forwards → snaps back.

---

## 3.8 animation-play-state

HTML:

<div class="pause-box"></div>

CSS:

.pause-box {
  width: 60px;
  height: 60px;
  background: black;

  animation: spin 1s linear infinite;
}

.pause-box:hover {
  animation-play-state: paused;
}

Hover → animation pauses.

---

## 4. Animation Shorthand (MOST USED)

HTML:

<div class="shorthand-box"></div>

CSS:

.shorthand-box {
  width: 60px;
  height: 60px;
  background: gold;

  animation: spin 2s linear infinite;
}

Equivalent to writing multiple properties.

---

## 5. Multiple Animations on One Element

HTML:

<div class="combo-box"></div>

CSS:

@keyframes float {
  from { transform: translateY(0); }
  to   { transform: translateY(-10px); }
}

.combo-box {
  width: 70px;
  height: 70px;
  background: #ff9a9e;

  animation:
    spin 2s linear infinite,
    float 0.6s ease-in-out infinite alternate;
}

Box spins AND floats.

---

## 6. Practical UI Patterns

---

## 6.1 Infinite Spinner (Loader)

HTML:

<div class="spinner"></div>

CSS:

.spinner {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: 4px solid #eee;
  border-top-color: #1f8ef1;

  animation: spin 1s linear infinite;
}

---

## 6.2 Pulse Effect (Attention Grabber)

HTML:

<button class="pulse-btn">Click Me</button>

CSS:

@keyframes pulseGlow {
  0%   { transform: scale(1); }
  50%  { transform: scale(1.05); }
  100% { transform: scale(1); }
}

.pulse-btn {
  animation: pulseGlow 1.2s ease-in-out infinite;
}

---

## 6.3 Slide-In on Load

HTML:

<h1 class="slide-title">Welcome</h1>

CSS:

@keyframes slideIn {
  from {
    transform: translateX(-40px);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.slide-title {
  animation: slideIn 0.6s ease-out forwards;
}

---

## 6.4 Fade-In on Load

HTML:

<p class="fade-text">Smooth appearance</p>

CSS:

.fade-text {
  animation: fadeIn 0.8s ease forwards;
}

---

## 7. Performance & Best Practices

### ✅ Prefer Animating

opacity  
transform  

Fast & smooth (GPU friendly).

---

### ⚠️ Avoid Heavy Animations On

width  
height  
top / left  

These trigger layout recalculation.

---

### ✅ Good Durations

Hover / micro-interactions → 0.15s – 0.3s  
Entrance animations → 0.3s – 0.7s  

Too slow → feels laggy.

---

### ✅ Use Fill Mode When Needed

forwards → keep final state  
both → best for intro animations

---

### ✅ Subtle > Flashy

Professional UI = restrained motion.

---

## 8. Cheat Sheet (Ultra Practical)

Define animation:

@keyframes spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}

Use animation:

.element {
  animation: spin 1s linear infinite;
}

Multiple animations:

animation:
  spin 2s linear infinite,
  float 0.6s ease infinite alternate;
