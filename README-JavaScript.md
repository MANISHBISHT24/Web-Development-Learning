# JavaScript Learning Notes

Core concepts of JavaScript — the language that makes webpages interactive.

## What is JavaScript

JavaScript webpage ko **behavior** deta hai — clicks handle karna, data
change karna, API se cheezein lana, page ko dynamically update karna.
HTML structure hai, CSS style hai, JS **logic** hai.

## Variables

```javascript
let age = 25;        // reassignable
const name = "Amit"; // cannot be reassigned
var old = "avoid";   // old syntax, avoid using
```

Prefer `const` by default, `let` jab value change karni ho. `var` avoid karo.

## Data Types

| Type | Example |
|---|---|
| String | `"hello"` |
| Number | `42`, `3.14` |
| Boolean | `true`, `false` |
| Array | `[1, 2, 3]` |
| Object | `{ name: "Amit", age: 25 }` |
| null / undefined | "no value" states |

## Functions

```javascript
// Regular function
function greet(name) {
  return `Hello, ${name}`;
}

// Arrow function (modern style)
const greet = (name) => `Hello, ${name}`;
```

## Arrays — Common Methods

```javascript
const nums = [1, 2, 3, 4, 5];

nums.map(n => n * 2);          // [2, 4, 6, 8, 10] — transform each item
nums.filter(n => n > 2);       // [3, 4, 5] — keep matching items
nums.reduce((sum, n) => sum + n, 0); // 15 — combine into one value
```

These three (`map`, `filter`, `reduce`) are used constantly — worth mastering early.

## DOM Manipulation

```javascript
const el = document.querySelector("#title");
el.textContent = "New Text";
el.classList.add("active");

document.querySelector("button").addEventListener("click", () => {
  console.log("Button clicked!");
});
```

- [ ] `querySelector` / `querySelectorAll` — elements select karna
- [ ] `textContent` / `innerHTML` — content change karna
- [ ] `addEventListener` — events handle karna (click, input, submit)
- [ ] `classList.add/remove/toggle` — classes manage karna (styling changes ke liye)

## Async JavaScript

```javascript
async function getData() {
  const response = await fetch("https://api.example.com/data");
  const data = await response.json();
  console.log(data);
}
```

- [ ] **Promise** — ek future value ka placeholder (pending/resolved/rejected)
- [ ] **async/await** — promises ko readable, synchronous-looking code jaisa likhna
- [ ] **fetch API** — server se data lena/bhejna

## ES6+ Features Worth Knowing

```javascript
// Destructuring
const { name, age } = person;

// Spread operator
const merged = [...arr1, ...arr2];

// Template literals
const msg = `Hello, ${name}!`;

// Default parameters
function greet(name = "Guest") { ... }
```

## Common Mistakes

- `var` use karna instead of `let`/`const`
- `==` use karna instead of `===` (type coercion se bugs aate hain)
- Async function ko `await` ke bina call karna
- Event listener ko galat element pe attach karna (existence check na karna)

## Practice Ideas

- To-do list app (add/remove/mark complete)
- Calculator
- Weather app (public API use karke)
- Quiz app with score tracking

## Resources

- [MDN JavaScript Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [JavaScript.info](https://javascript.info/)
- [freeCodeCamp — JS Algorithms](https://www.freecodecamp.org/)
