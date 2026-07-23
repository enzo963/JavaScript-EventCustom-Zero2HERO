# Course Roadmap

---

## Phase 1 (Completed)

- What is an Event
- `addEventListener()`
- `CustomEvent`
- `dispatchEvent()`
- `detail`
- `bubbles`

---

## Phase 2 (Current)

1. `event.target`
2. `event.currentTarget`
3. The difference between them (one of the most common JavaScript interview questions)

---

## Phase 3

1. `stopPropagation()`
   - How to stop an event from bubbling.
   - Its relationship with `bubbles`.

2. `preventDefault()`
   - One of the most frequently used methods in JavaScript.
   - Why we use it with forms (`submit`) and links (`<a>`).

3. The difference between:
   - `stopPropagation()`
   - `preventDefault()`
   - `stopImmediatePropagation()`

---

## Phase 4

1. Event Delegation
   - One of the most powerful techniques in JavaScript.
   - How to manage **1,000 elements** using only **one Event Listener**.
   - Widely used in large-scale applications and many JavaScript libraries.

---

## Phase 5

1. `addEventListener()` Options

- `once`
- `capture`
- `passive`
- `signal` *(the newest option)*

Example:

```js
button.addEventListener("click", handler, {
    once: true
});
```

---

## Phase 6

1. Build a complete event system between application components.
2. Learn how to use Custom Events in real-world projects.
3. Understand how frameworks like **React** and **Vue** handle events *(conceptually)*.

---

# Final Practical Project

We won't finish this course until we build a real project using everything we've learned.

Possible projects include:

- Notification System
- Shopping Cart
- Chat App
- Game UI
- Dashboard

By the end, you'll understand how different parts of an application communicate with each other through events.

---

# 📂 Chapters

| Chapter | Topic |
|---------|-------|
| Chapter 1 | [[Chapter1 - Custom Event for beginners]] |
| Chapter 2 | [[Chapter2 - Custom Event for intermediate]] |
| Chapter 3 | [[Chapter3 - Event Bubbling]] |
| Chapter 4 | [[Chapter4 - Event Object]] |
| Chapter 5 | [[Chapter5 - event.target vs event.currentTarget]] |
