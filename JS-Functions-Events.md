# JavaScript Functions & Events — Learning Notes

Core concepts of functions (reusable code) and events (reacting to the user).

## What is a Function

A function is a **reusable block of code** that does one job. Write it once,
run it (call it) as many times as you need.

```javascript
function greet() {
  console.log("Hello!");
}

greet(); // "calling" the function
greet(); // can call it again anytime
```

Writing a function does nothing on its own — it only runs when you **call** it.

## Why Use Functions

- **Reusability** — write once, use many times
- **Maintainability** — fix a bug in one place, not ten
- **Organised code** — each job lives in its own box
- **Easier debugging** — problems are easy to locate
- **Better readability** — a good name explains what it does
- **Unit testing** — small pieces are easy to test on their own

## What Makes a Good Function

- Does **one job** (single responsibility)
- Kept **short** — around 20–30 lines is a good target
- If it grows too big, **split it** into smaller functions

> Rule of thumb: if you can't describe what a function does in one short
> sentence, it's probably doing too much.

## Parts of a Function

```javascript
function add(a, b) {   // a, b = parameters (placeholders)
  return a + b;         // return = send a value back
}

let total = add(2, 3);  // 2, 3 = arguments (real values) -> total is 5
```

**Easy way to remember**: Parameters are the **P**laceholders. Arguments are
the **A**ctual values.

## The `return` Statement

`return` sends a value back and **stops the function right there**.

```javascript
function square(n) {
  return n * n;
  console.log("never runs"); // dead code — never executes
}
```

Functions without `return` still work fine — they just hand back `undefined`.
That's okay when you don't need a value back (e.g. printing to the screen).

## Function vs Procedure

| | Takes input, returns a value | Just does a job |
|---|---|---|
| Traditional term | Function | Procedure |
| In JavaScript | Called "function" | Also called "function" |

JavaScript doesn't have a separate `procedure` keyword — both are written
the same way, one just skips the `return`.

## Pure vs Impure Functions

```javascript
// Pure — same input always gives same output, no outside changes
function add(a, b) {
  return a + b;
}

// Impure — changes something outside itself
let count = 0;
function tick() {
  count++;
}
```

| Pure | Impure |
|---|---|
| Same input → same output | Output can change with same input |
| No side effects | Touches DOM, globals, random, time |
| Easy to test and trust | Harder to test |

Aim for pure functions where you can — they're predictable, so bugs are rarer.

## Three Ways to Write a Function

```javascript
// 1. Function declaration
function greet(name) {
  return "Hi " + name;
}

// 2. Function expression
const greet = function (name) {
  return "Hi " + name;
};

// 3. Arrow function
const greet = (name) => {
  return "Hi " + name;
};
```

## Arrow Function Shortcuts

```javascript
// Implicit return (single expression, no braces/return keyword needed)
const add = (a, b) => a + b;

// Single parameter — brackets optional
const square = n => n * n;

// Multiple parameters — brackets required
const add = (a, b) => a + b;
```

**Same function, 5 ways** (all equal):
```javascript
function add(a, b) { return a + b; }
const add = function(a, b) { return a + b; };
const add = (a, b) => { return a + b; };
const add = (a, b) => a + b;
```

Quick guide: one line of logic → implicit return. One parameter → drop the
`()`. Zero or 2+ parameters → keep the `()`.

---

## Events — Reacting to the User

An **event** is something that happens on the page: a click, a key press,
mouse movement, a form submit. Attaching a function to run when it happens
is what makes a page interactive.

## `addEventListener`

```javascript
btn.addEventListener("click", () => {
  console.log("clicked!");
});
```

The function you pass is a **callback** — the browser calls it back when
the event fires. You can pass a named function too:

```javascript
function changeColor() { ... }
btn.addEventListener("mouseout", changeColor);
```

⚠️ **Watch out**: pass the function name **without** brackets
(`changeColor`), not `changeColor()`. Brackets run it immediately instead
of waiting for the event.

## The Event Object

```javascript
btn.addEventListener("click", (event) => {
  console.log(event.target); // the element clicked
  console.log(event.type);   // "click"
});
```

## Common Events

| Event | Fires when... |
|---|---|
| `click` | An element is clicked |
| `dblclick` | An element is double-clicked |
| `mouseover` / `mouseout` | Mouse enters / leaves an element |
| `mousemove` | Mouse moves over an element |
| `keydown` / `keyup` | A key is pressed / released |
| `input` | A field's value changes as you type |
| `change` | A field changes and loses focus |
| `submit` | A form is submitted |
| `blur` | An element loses focus |
| `scroll` | The user scrolls |
| `resize` | The window is resized |
| `load` | The page (or an image) finishes loading |

## The Pattern: Select → Listen → Do

```javascript
// 1. Select
const btn = document.querySelector(".btn");

// 2. Write the handler
function changeBackgroundColor() {
  document.body.style.background = "lightblue";
}

// 3. Listen, and pass the handler as a callback
btn.addEventListener("mouseout", changeBackgroundColor);
```

Almost every interactive feature on the web is this loop — different event,
different action.

## Removing an Event Listener

```javascript
btn.addEventListener("click", changeColor);

// later
btn.removeEventListener("click", changeColor);
```

**Why remove one:**
- One-time actions (e.g. a "claim reward" button)
- Cleanup — when an element goes away, remove its listeners
- Turning behaviour off once something is done or disabled

⚠️ **Important**: only works with the **same named function**. An inline
arrow function (`() => {...}`) is a new function every time, so the browser
can't find it to remove it. Use a named function if you plan to remove it.

## Graceful Degradation

JavaScript can be switched off or fail to load — a page should still make
sense without it.

- Write real HTML content and real links **first**
- Use JS to **enhance**, not to hold the whole page together
- If JS is the only thing making a page usable, users without it see a
  broken page

**Testing tip**: Open DevTools (F12) → Settings/command menu → toggle
"Disable JavaScript." Reload and see what still works. If the content
still reads and links still work, the page is built well.

---

## Key Takeaways

- A function should do one thing, and its name should tell you what
- Parameters are placeholders, arguments are the real values
- Pass a callback **by name** (no brackets) to `addEventListener`
- To remove a listener you need the **same named function**
- Every interactive feature = **select, listen, do**

## Practice Ideas

- A button that toggles dark/light mode on click
- A form that validates input on `submit`
- A color-change on `mouseover` / `mouseout`
- A character counter that updates on `input`

## Resources

- [MDN — addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
- [MDN — Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
- [JavaScript.info — Events](https://javascript.info/events)
