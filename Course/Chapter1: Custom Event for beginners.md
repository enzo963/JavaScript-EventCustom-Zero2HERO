````md
# The usual events in JS

    - click
    - input
    - submit
    - keydown
    - mousemove

All of these events and we call it ** Built -in Events **.

But what if we want create events by our selves like:

```text
playerDead

userLogin

cartUpdated

themeChanged

courseFinished
````

In **JS** we can create events.

So now we have **2 types of events in JS**:

1. Event in JS by default
2. Custom Event - you create it in JS

---

# Keywords

### 1. Event

### 2. CustomEvent

### 3. dispatchEvent()

* This is the most important keyword in JS.
* Its function is to trigger the event.

### 4. addEventListener()

* This keyword works with `CustomEvent`.

### 5. new CustomEvent()

* This creates the event for the first time.

### 6. detail

* This is the most important.

---

# dispatchEvent()

### Example

```js
button.dispatchEvent(event);

// Run this event now.
```

---

# addEventListener()

### Example

```js
button.addEventListener("gameOver", ...);

// if
```

---

# new CustomEvent()

### Example

```js
const event = new CustomEvent("gameOver");

// Now you have an event -> gameOver
```

---

# detail

### Example

```js
detail
    |
    v

// These are the data you may send inside the message like:

// 1- score: 900
// 2- username: Enzo
// 3- theme: dark

// The form is like this:

new CustomEvent("login", {
    detail: {
        name: "ENZO"
    }
});

// And inside the listener:

button.addEventListener("", (event) => {
    console.log(event.detail);

    // OR

    console.log(event.detail);
});
```

---

# So now we have

| **Keyword**      | **The Function**              |
| ---------------- | ----------------------------- |
| Event            | Which event                   |
| CustomEvent      | An event from your own making |
| dispatchEvent    | Trigger the event             |
| addEventListener | Waiting for the event         |
| detail           | Load data                     |
| event.detail     | Read data                     |

---

# Examples

# Example 1

```js
const btn = document.getElementById("btn");

btn.addEventListener("hello", () => {
    console.log("Hello Event!");
});

const myEvent = new CustomEvent("hello");

btn.dispatchEvent(myEvent);
```

So what's happen here:

```text
1 - We create the Event
    |
    v
2 - hello
    |
    v
3 - We listened to it
    |
    v
4 - We trigger it
    |
    v
5 - The Result
    ```

```js
Hello Event!
    ```

---

# Example 2 - Change the name

```js
const alarm = new CustomEvent("alarm");

document.addEventListener("alarm", () => {
    console.log("Danger!");
});

document.dispatchEvent(alarm);

// The Result is - Danger! -
```

---

# Example 3 - Send Data

```js
// Send the data

const loginEvent = new CustomEvent("login", {
    detail: {
        username: "ENZO"
    }
});

// Now we have to listen for this event (data)

document.addEventListener("login", (e) => {
    console.log(e.detail.username);
});

// Now we have to run this event

document.dispatchEvent(loginEvent);

// The Result

ENZO
    ```

---

# Example 4 - Send a lot of Data

```js
// Send

const scoreEvent = new CustomEvent("gameFinished", {
    detail: {
        player: "Enzo",
        score: 900,
        level: 15
    }
});

// Listener

document.addEventListener("gameFinished", (e) => {
    console.log(e.detail.player);
    console.log(e.detail.score);
    console.log(e.detail.level);
});

// The Result

/*
Enzo
900
15
*/
```

---

# Example 5 - Real example (Store)

```js
// Send

const cartUpdated = new CustomEvent("cartUpdated", {
    detail: {
        items: 5
    }
});

// Listener

document.addEventListener("cartUpdated", (e) => {
    console.log(`Item: ${e.detail.items}`);
});

document.dispatchEvent(cartUpdated);
```

---

# Example 6 - Many listeners for one event

```js
const event = new CustomEvent("gameOver");

document.addEventListener("gameOver", () => {
    console.log("Show Game Over screen");
});

document.addEventListener("gameOver", () => {
    console.log("Play sad music");
});

document.addEventListener("gameOver", () => {
    console.log("Save score");
});

document.dispatchEvent(event);
```

```
    ```
