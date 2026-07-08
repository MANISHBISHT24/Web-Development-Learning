# HTML Learning Notes

Core concepts of HTML — the structure/skeleton of every webpage.

## What is HTML

HTML (HyperText Markup Language) webpage ka **structure** define karta hai —
kaunsa content kahan hai, aur uska meaning kya hai (heading hai, paragraph
hai, list hai, etc.). Ye styling ya behavior nahi handle karta — wo CSS aur
JS ka kaam hai.

## Basic Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Page Title</title>
</head>
<body>
  <!-- visible content goes here -->
</body>
</html>
```

- [ ] `<!DOCTYPE html>` — browser ko batata hai ye HTML5 document hai
- [ ] `<head>` — metadata, title, linked CSS/fonts (khud kuch dikhta nahi)
- [ ] `<body>` — jo kuch bhi page pe dikhta hai, wahi yahan hota hai

## Semantic Tags (Important!)

Semantic tags meaning carry karte hain, `<div>` sirf ek generic box hai.

| Tag | Use |
|---|---|
| `<header>` | Page/section ka top part (logo, nav) |
| `<nav>` | Navigation links |
| `<main>` | Page ka main content |
| `<section>` | Content ka logical group |
| `<article>` | Independent, standalone content (blog post, card) |
| `<footer>` | Page/section ka bottom part |
| `<h1>`–`<h6>` | Headings (sirf ek `<h1>` per page rakho) |

**Kyun important hai**: Screen readers, SEO, aur code readability — sab semantic tags se behtar hote hain `div` soup se.

## Common Elements

- [ ] Text: `<p>`, `<span>`, `<strong>`, `<em>`
- [ ] Lists: `<ul>`, `<ol>`, `<li>`
- [ ] Links & images: `<a href="">`, `<img src="" alt="">`
- [ ] Forms: `<form>`, `<input>`, `<label>`, `<button>`, `<select>`
- [ ] Tables: `<table>`, `<tr>`, `<td>`, `<th>`

## Forms — Quick Reference

```html
<form>
  <label for="email">Email</label>
  <input id="email" type="email" placeholder="you@example.com" required />
  <button type="submit">Submit</button>
</form>
```

- Har `<input>` ka apna `<label>` hona chahiye (accessibility ke liye)
- `type` attribute important hai: `text`, `email`, `password`, `number`, `checkbox`, `radio`

## Accessibility Basics

- [ ] Har `<img>` mein `alt` text ho
- [ ] Headings logical order mein ho (`h1` → `h2` → `h3`, skip mat karo)
- [ ] Form inputs `<label>` se linked ho
- [ ] Color hi ekmatra way na ho information dene ka

## Common Mistakes

- Divs ka bahut zyada use karna jab semantic tag fit karta ho
- Multiple `<h1>` ek page mein
- `alt` text missing images pe
- Closing tags bhoolna (`<li>` khula rehna, etc.)

## Practice Ideas

- Personal portfolio page
- Recipe card page
- Simple contact form (bina JS ke)

## Resources

- [MDN HTML Docs](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [freeCodeCamp — Responsive Web Design](https://www.freecodecamp.org/)
