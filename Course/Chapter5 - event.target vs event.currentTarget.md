
I want you to forget **JavaScript** for a one minute.

Imagen this scene

```ruby

Mall 
 | 
 |-- Family
  |
  |-- Child

```

The Child pressed the **alarm** button.

Who's pressed ? : **Child**

but who heard the sound ? : family and the whole mall
This's the concept  of **Event Bubbling**

## Now we'll see where the turn comes

- ## 1- event.target

- ## 2- event.currentTarget

First what's the **event.target**
Note this : **target** --> Who started the event for the first time.

## Example 1

```html

<div id="parent">  
  
 <button id="btn">  
  Click Me  
 </button>  
  
</div>


<!-- 

parent  
|  
└── button

->
```
```js

const parent = document.getElemntById("parent");
const button = document.getElemntById("button");

parent.addEventListener("click", (e)=>{
	console.log(e.target);
});

```

Now Press the button.
The question : **What is the result?**

Most people say: **parent**

The actual result: **button**

Why?... Because
**target** -> means

- Who initiated the event?
- And who initiated it?

$$
button
$$

---

## Example 2

```html
<div id="box">

    <h1>Hello</h1>

</div>
```
```js
box.addEventListener("click",(e)=>{

	console.log(e.target);

});
```
If you click on -> Hello

the result is: **h1** ---> not **div**
So, target always refers to the element that the **user clicked**.

---

## Now, what is `currentTarget`?

This is different.
Remember this sentence:
`currentTarget` = the element the listener is currently acting upon.

## Same Example 1

```html

<div id="parent">  
  
 <button id="btn">  
  Click Me  
 </button>  
  
</div>

<!-- 
                            parent  
                              |  
                              └── button
->
```

```js
const parent = document.getElemntById("parent");
const button = document.getElemntById("button");

parent.addEventListener("click", (e)=>{
 console.log(e.currentTarget);
});
```

Press the button. Result : **parent**
Why?... Because the listener is on : -> **parent**

## Example 3

```html
<div id="parent">

 <button id="btn">
  Click
 </button>
</div>
```

```js
parent.document.addEventListener("click",(e)=>{
 console.log("Target);
 console.log(e.target);
 console.log("Currnet");
 console.log(e.currentTarget);
});

// The Result -> Click on Button 
- Target  
-- button  
- Current   
-- parent


// The Result -> Click on Parant
- Target  
-- parent  
- Current   
-- parent


```

---

## Example 4

```html
<ul id="menu">
 <li>Home</li>
 <li>About</li>
 <li>Contact</li>
</ul>
```

```js
menu.addEventListener("click",(e)=>{
 console.log(e.target);
});

// Result 
- li // not -> ul

//But iiiiiffffffffffffffffffffffffffffffffff

menu.addEventListener("click",(e)=>{
 console.log(e.cuurentTarget);
});

//Reult
ul
```

---

## Example 5

```html
<ul id="menu">
 <li>Home</li>
 <li>About</li>
 <li>Contact</li>
</ul>
```

```js
menu.addEventListener("click", (e) => {  
 console.log("You clicked:", e.target.textContent);  
});


/* The Result if user click */ -> Home 

You clicked: Home

/* The Result if user click */ -> Contact
 
You clicked: Contact

// all of this in the same
```

---

## Note

**The target**: does not care where the listener is located.
**The target**: only cares: Who initiated the event?

## Funny Example

👨 Father ← Listener here
 │
 ├── 👦 Son ← Click

Who clicked?: 👦 Son
    |
    v

```
event.target
```

Who is listening?: 👨 Father
    |
    v

```
event.currentTarget
```

---

## Example 6

```html
<div id="grand"> 
  
 <div id="parent">  
     
  <button id="btn">  
   Click  
  </button>  
   </div>  
</div>
```

```js
grand.addEventListener("click", (e) => {  
 console.log("Grand");  
});  
  
parent.addEventListener("click", (e) => {  
 console.log("Parent");  
});  
  
btn.addEventListener("click", (e) => {  
 console.log("Button");  
});

//The Result 

User Click  
│  
▼  
+------------+  
| Button     | ← أول Listener  
+------------+  
▲  
│ Bubble  
+------------+  
| Parent     | ← ثاني Listener  
+------------+  
▲  
│ Bubble  
+------------+  
| Grand      | ← ثالث Listener  
+------------+

```
