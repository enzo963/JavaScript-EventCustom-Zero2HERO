# Chapter 2 — Why Do We Need `CustomEvent`?

The first question is:

> **Why don't we just use a normal function?**

Let's assume we have this code:

```js
function showMessage() {
    console.log("Hello");
}

showMessage();

// Result:
// Hello
```

Did we need **CustomEvent** here?

> **No.**

---

## So, Why Does `CustomEvent` Exist?

Because sometimes the part that **triggers** the event doesn't know **who is listening**.

---

# Example 1

Imagine we have a video game.

```
Player
   │
   ▼
 died
```

Now...

What should happen?

- Play the game over music
- Display **"Game Over"**
- Save the score
- Stop the timer
- Send the data to the server

If we use a normal function, we have to write everything manually.

```js
function playerDead() {
    showGameOver();
    playMusic();
    saveScore();
    stopTimer();
    sendServer();
}
```

Now imagine we want to add another function:

```js
showAnimation();
```

We must go back and modify `playerDead()` again.

---

## With `CustomEvent`

Instead, we only announce that the player died.

```js
document.dispatchEvent(
    new CustomEvent("playerDead")
);
```

That's it.

Anyone interested in this event simply listens for it.

```js
document.addEventListener("playerDead", showGameOver);
```

```js
document.addEventListener("playerDead", playMusic);
```

```js
document.addEventListener("playerDead", saveScore);
```

```js
document.addEventListener("playerDead", stopTimer);
```

Every listener is completely independent.

---

## Think About It

A **function** says:

> Go run this specific code.

A **CustomEvent** says:

> Hey everyone! Something happened.
>
> Whoever cares can handle it.

This is one of the biggest concepts in programming.

---

# An Important Question

## Who reads the event name?

**You do.**

So you can write any event name you want.

```js
new CustomEvent("pizzaReady");
```

or

```js
new CustomEvent("enemyDead");
```

or

```js
new CustomEvent("themeChanged");
```

or

```js
new CustomEvent("loginSuccess");
```

---

# Example

```js
// Create event
const event = new CustomEvent("coffeeReady");

// Listen
document.addEventListener("coffeeReady", () => {
    console.log("Drink!");
});

// Dispatch
document.dispatchEvent(event);

// Result
// Drink!
```

> **Notice**
>
> JavaScript does **not** know what `coffeeReady` means.
>
> **You invented it.**

---

# Another Important Question

## Why do we write `document` instead of `button`?

Because almost every DOM object can dispatch and listen to events.

For example:

```text
button
div
span
input
body
document
window
```

All of these can have events.

---

# Example 2

```js
const box = document.querySelector(".box");

box.addEventListener(...);

box.dispatchEvent(...);
```

So, events are **not** specific to `document`.

---

# Example 3

```html
<div class="card"></div>
```

```js
// Create variable
const card = document.querySelector(".card");

// Listen
card.addEventListener("flip", () => {
    console.log("Card Flipped");
});

// Dispatch
card.dispatchEvent(
    new CustomEvent("flip")
);

// Result
// Card Flipped
```

> **Notice**
>
> This event now belongs only to the card.

---

# Another Important Question

## Why do we have `click`, but also `dispatchEvent()`?

Because `click` is a **natural browser event**.

It comes from the user.

```text
+----------------+
|      User      |
|        ↓       |
|     Click      |
|        ↓       |
|    Browser     |
|        ↓       |
|      Event     |
+----------------+
```

---

`dispatchEvent()` is different.

You create and dispatch the event yourself.

```text
+----------------------+
|      JavaScript      |
|          ↓           |
|   dispatchEvent()    |
|          ↓           |
|        Event         |
+----------------------+
```

---

# Example 4

```html
<button>Save</button>
```

If the user clicks the button:

```js
button.dispatchEvent(
    new CustomEvent("saveDone")
);
```

The `saveDone` event was **not** created by the browser.

**You created it.**

---

# Function vs Custom Event

| Function | Custom Event |
|-----------|--------------|
| Executes something directly. | Announces that something happened. |
| You know exactly what you're calling. | You don't need to know who is listening. |
| Tight Coupling | Loose Coupling |
| Good for small projects. | Excellent for large-scale applications. |

---

# Real-Life Analogy

Imagine a university.

When a student graduates, there are two ways to handle it.

---

## Method 1 — Functions

The teacher contacts everyone manually.

```text
Teacher
   │
   ├── Accounting
   ├── Library
   ├── Administration
   └── Archives
```

Every time a student graduates, the teacher must contact everyone again.

---

## Method 2 — Custom Events

The teacher simply announces:

> "The student has graduated."

Then everyone who cares reacts.

- Accounting updates the records.
- The library clears borrowed books.
- The alumni department creates an account.
- The documentation department archives the student's file.

The teacher **doesn't know** who is listening.

The teacher **doesn't care** who reacts.

The teacher only announces that something happened.

---

# The Core Idea

**Custom Events decouple your code.**

Instead of one object controlling everything, every component becomes independent.

This makes your applications:

- Easier to maintain
- Easier to extend
- Easier to test
- Easier to scale
