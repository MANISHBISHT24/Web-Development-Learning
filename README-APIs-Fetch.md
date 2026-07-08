# Working with APIs & Fetch — Learning Notes

*Full-Stack Internship · Module 1 · Day 10 · Instructor: Dinesh Rawat*

Core concepts of APIs, HTTP, and using `fetch()` to talk to servers.

## What is an API — The Restaurant Analogy

- **You (client)** — order food, don't go into the kitchen yourself
- **API (waiter)** — takes your order to the kitchen, brings the food back
- **Server (kitchen)** — prepares the actual food (data/response)

An API is the middleman that lets a client ask a server for something,
without needing to know how the server works internally.

## Client and Server

- The **client always speaks first** — the server never initiates
- **One request gives one response** — you ask, you get an answer back

## Anatomy of a Request

| Part | What it is |
|---|---|
| **Method** | The action — GET, POST, PUT, PATCH, DELETE |
| **URL** | Where the request is going |
| **Headers** | Metadata — content type, auth tokens, etc. |
| **Body** | The actual data being sent (not used with GET) |

## Anatomy of a Response

| Part | What it is |
|---|---|
| **Status** | A code telling you what happened (200, 404, 500...) |
| **Headers** | Metadata about the response |
| **Body** | The actual data returned |

> **Read the status code first — a body can lie.** A response body might
> look like valid data even when something went wrong; the status code is
> the source of truth for what actually happened.

## JSON — The Data Format

JSON (JavaScript Object Notation) is the standard format APIs use to send
data.

```javascript
// Parsing a response body into a JS object
const data = await response.json();

// Converting a JS object into a string to send
const body = JSON.stringify({ name: "Amit", age: 25 });
```

## The Five HTTP Methods

| Method | Action |
|---|---|
| `GET` | Read data |
| `POST` | Create new data |
| `PUT` | Replace data entirely |
| `PATCH` | Update part of the data |
| `DELETE` | Remove data |

## GET vs POST

| | GET | POST |
|---|---|---|
| Data location | In the URL (query params) | In the request body |
| Visible in URL | Yes | No |
| Safe to repeat | Yes (idempotent) | **No** — repeating can create duplicates (e.g. submitting an order twice) |

## Status Code Families

| Range | Meaning |
|---|---|
| `1xx` | Informational |
| `2xx` | Success |
| `3xx` | Redirection |
| `4xx` | Client error (you made a mistake) |
| `5xx` | Server error (the server made a mistake) |

### Everyday Status Codes

| Code | Meaning |
|---|---|
| `200` | OK — success |
| `201` | Created — new resource made (after a POST) |
| `204` | No Content — success, nothing to return |
| `400` | Bad Request — your request was malformed |
| `401` | Unauthorized — you're not logged in / no valid token |
| `403` | Forbidden — you're logged in but not allowed |
| `404` | Not Found |
| `429` | Too Many Requests — rate limited |
| `500` | Internal Server Error |

## REST URL Design

> **URLs are nouns, methods are verbs.**

```
GET    /users          → get all users
GET    /users/5        → get user with id 5
POST   /users          → create a new user
PUT    /users/5        → replace user 5 entirely
PATCH  /users/5        → update part of user 5
DELETE /users/5        → delete user 5
```

Don't put verbs in the URL (`/getUsers`, `/deleteUser5`) — the HTTP method
already says what action is happening.

## Using `fetch()`

### With `.then()`

```javascript
fetch("https://api.example.com/users")
  .then(res => res.json())
  .then(data => console.log(data));
```

### With `async/await` (cleaner)

```javascript
async function getUsers() {
  const res = await fetch("https://api.example.com/users");
  const data = await res.json();
  console.log(data);
}
```

**Why await twice?** `fetch()` resolves once the response *headers* arrive
— the body may still be streaming in. `res.json()` is itself async because
it has to wait for and parse that body. So you `await` the fetch, then
`await` the `.json()` call separately.

## Sending Data with `fetch()`

```javascript
async function createUser(user) {
  const res = await fetch("https://api.example.com/users", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(user),
  });
  const data = await res.json();
  return data;
}
```

## Error Handling

⚠️ **`fetch()` does NOT throw an error on 404 or 500** — it only throws on
a network failure (e.g. no internet, DNS failure). A 404 or 500 still
resolves successfully as far as `fetch` is concerned.

**Always check `res.ok` yourself:**

```javascript
async function getUsers() {
  const res = await fetch("https://api.example.com/users");

  if (!res.ok) {
    throw new Error(`Request failed: ${res.status}`);
  }

  return res.json();
}
```

`res.ok` is `true` for any `2xx` status, `false` otherwise.

## Auth Basics

- **API keys** — a simple secret string identifying your app
- **Bearer tokens** — sent in the `Authorization` header:
  ```
  Authorization: Bearer <token>
  ```

⚠️ **Keep secret keys in `.env` files — never in git, never in frontend
code.** Frontend code is visible to anyone who opens DevTools; anything
sent to the browser is effectively public.

```
# .env
API_KEY=your_secret_key_here
```

```
# .gitignore
.env
```

## The Other Side — Express (Server)

```javascript
const express = require("express");
const app = express();
app.use(express.json());

app.get("/users", (req, res) => {
  res.status(200).json({ users: [] });
});

app.post("/users", (req, res) => {
  const newUser = req.body;
  res.status(201).json(newUser);
});
```

- `app.get()` / `app.post()` — define routes for each HTTP method
- `res.status().json()` — set the status code and send a JSON response

## Live Demo Reference

The class used the [PokeAPI](https://pokeapi.co/) in the browser console
to practice real `fetch()` calls against a live public API.

---

## Key Takeaways

- **Read the status code first** — the body can lie about what happened
- `fetch()` only throws on **network failure** — always check `res.ok` yourself
- **URLs are nouns, methods are verbs**
- **Secret keys never go in frontend code or git**

## Practice Ideas

- Fetch data from a free public API (PokeAPI, JSONPlaceholder, OpenWeather) and display it on a page
- Build a small Express server with GET and POST routes
- Write a `fetch` wrapper function that throws a proper error when `res.ok` is false
- Practice sending a POST request with a JSON body and reading back the response

## Resources

- [MDN — Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- [MDN — HTTP Response Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [PokeAPI](https://pokeapi.co/) — free API to practice with
- [JSONPlaceholder](https://jsonplaceholder.typicode.com/) — free fake REST API for testing
