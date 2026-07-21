# Chapter 3 — `bubbles`

If you understand this lesson, you'll understand **why the `bubbles` option exists.**

---

# First of All

## What does **"Bubble"** mean?

Imagine you have this HTML code:

```html
<body>

    <div id="parent">
        <button id="btn">
            Click
        </button>
    </div>

</body>
```

The structure looks like a tree.

```text
body
│
└── parent
      │
      └── button
```

Each element lives inside another element.

---

# What Happens When the Button Is Clicked?

You clicked on:

```text
button
```

But...

Does the event stay inside the button?

> **No!**

It travels upward.

```text
button
   ↑
parent
   ↑
body
   ↑
document
```

This behavior is called **Event Bubbling**.

---

# Example 1

```html
<div id="parent">

    <button id="btn">
        Click
    </button>

</div>
```

```js
const parent = document.getElementById("parent");
const btn = document.getElementById("btn");

btn.addEventListener("click", () => {
    console.log("Button");
});

parent.addEventListener("click", () => {
    console.log("Parent");
});
```

---

## Question

If you click the button...

What do you expect?

Many beginners answer:

```text
Button
```

But the real result is:

```text
Button
Parent
```

### Why?

Because the event starts at the button...

Then it **bubbles** to its parent.

---

# Example 2

```html
<body>

    <div id="parent">
        <button id="btn">Click</button>
    </div>

</body>
```

```js
btn.addEventListener("click", () => {
    console.log("Button");
});

parent.addEventListener("click", () => {
    console.log("Parent");
});

document.body.addEventListener("click", () => {
    console.log("Body");
});
```

Result:

```text
Button
Parent
Body
```

> **Notice**
>
> All three listeners ran because the event bubbled upward.

---

# An Important Question

Can a **Custom Event** do the same thing?

**Yes.**

But...

**Not always.**

---

# Example 3

```js
btn.dispatchEvent(
    new CustomEvent("hello")
);

// Listener
parent.addEventListener("hello", () => {
    console.log("Parent");
});
```

Will it work?

> **No.**

### Why?

Because by default:

```text
CustomEvent
↓
bubbles = false
```

That means the event **doesn't move up** to the parent.

---

## The Solution

Enable bubbling.

```js
new CustomEvent("hello", {
    bubbles: true
});
```

Now the event can travel upward.

---

# Complete Example

```js
const event = new CustomEvent("hello", {
    bubbles: true
});

btn.dispatchEvent(event);

// Listener
parent.addEventListener("hello", () => {
    console.log("Parent Heard It");
});

// Result
// Parent Heard It
```

---

# Visual Comparison

Without `bubbles: true`

```text
button
```

The event stays inside the button.

---

With `bubbles: true`

```text
button
   ↑
parent
   ↑
body
   ↑
document
```

Now every parent can hear the event.

---

# Why Is This Useful?

Imagine you have **500 buttons**.

Without bubbling, you might write:

```js
button1.addEventListener(...);

button2.addEventListener(...);

button3.addEventListener(...);

// ...

button500.addEventListener(...);
```

That's a lot of repeated code.

Instead...

Listen only once on the parent.

```js
parent.addEventListener("click", () => {
    console.log("One listener for all buttons.");
});
```

As long as the events bubble up, the parent can handle them.

This technique is called:

> **Event Delegation**

---

# Summary

## `bubbles`

Determines whether an event travels upward through its parent elements.

| Value | Behavior |
|--------|----------|
| `bubbles: true` | The event bubbles to parent elements. |
| `bubbles: false` | The event stays inside the current element. |

---

# Flow Diagram

Without bubbling:

```text
button
```

With bubbling:

```text
button
   ↑
parent
   ↑
body
   ↑
document
```

That's exactly what the `bubbles` option controls.
