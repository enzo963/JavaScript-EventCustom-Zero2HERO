
Before we learn about `event.target` or `event.currentTarget`,
we need to understand something more important.

What dose Event Object is ?

```html
<button>Click</button>
```

And you do.

```js
button.addEventListener("click", ()=>{
 console.log("Hello");
});
```

The question...

- How does JavaScript know which button you pressed?
- How does it know the time?
- How does it know the mouse's location?
- How does it know the type of event?

The **Answer**...
Because it creates an object called an **Event Object** every time an event occurs.

## Mental image

```js
  User Click  
         ↓  
      Browser  
         ↓  
 Create Event Object  
   ↓  
And send it to Listener

```

So, every event creates a new object.

---

## Example 1

```js
button.addEventListener("cilck",(event)=>{
 console.log(event);
});
```

We wrote **event**

Where did it come from?. We didn't create it.
**JavaScript** gave it to us.

If you press the button,

(in console). something like this will appear:

```js
PointerEvent {  

isTrusted:true,  
type:"click",  
target:button,  

}
```

You might see dozens of properties.

**Very important:**

The word: `event` is not a reserved word.

You can write

```js
button.addEventListener("click",(banana)=>{
 console.log(banana);
});
```

It will work.

OR

```js
button.addEventListener("click",(x)=>{  
 console.log(x);  
});
```

it work.

EVEN

```js
bitton.addEventListener("dog",(dog)=>{
 console.log(dog);
});
```

This is just a variable name.
But almost the entire world uses. **event** or **e**

```js
button.addEventListener("click",(e)=>{  
 console.log(e);  
});
```

This is the most widespread.

## What does the Event Object contain?

A great many things.

**Such as...**

```js
type  
target  
currentTarget  
clientX  
clientY  
pageX  
pageY  
button  
key  
code  
timeStamp  
defaultPrevented  
bubbles  
cancelable
```

It may contain more than 100 properties, depending on the event type.

## Example 2

```js
button.addEventListener("click",(e)=>{  
 console.log(e.type);  
});

//The Reuslt 
click

//If it was 
keydown

// So 

console.log(e.type );
// It gives me the name of the event.

```

## Example 3

```js

input.addEventListener("input",(e)=>{
 console.log(e.type);
});

//The Reuslt 
input 

```

## Example 4

```js

document.addEventListener("keydown",(e)=>{
 console.log(e.type);
});

click any button // The Reuslt 

keydown

```

##### An Another Properties

- timeStamp

## Example 5

```js
button.addEventListener("click",(e)=>{
 console.log(e.timeStamp);
});

// The Reuslt 
3245.6
//OR
9200.3

and this is the time when we created the event 


```

Properties 3

- isTrusted
If the user presses the button themselves.

```js
Mouse  
  ↓  
Click

// The Result 
true


--- --- --- --- --- --- --- --- --- --- ---
but if you write

buuton.click();

//The result 
flase

```

Because the user didn't click. It was JavaScript that clicked.

## Example 6

```js
button.addEventListener("click",(e)=>{  
 console.log(e.isTrusted);  
});

true 

button.click();
flase 

```

Why is this useful?
Some web sites want to ensure that the user performed the action themselves,
rather than a script.

---

###### Lesson Summary

| words          | Its benefit                                                                   |
| -------------- | ----------------------------------------------------------------------------- |
| `event` or `e` | An object containing event information.                                       |
| `e.type`       | Event Name (`click`, `keydown`, `input`...).                                  |
| `e.timeStamp`  | Event creation time.                                                          |
| `e.isTrusted`  | Did the event originate from the user? (`true`) Or from JavaScript (`false`). |
