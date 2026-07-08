# CSS Learning Notes

Core concepts of CSS — styling and layout for the web.

## What is CSS

CSS (Cascading Style Sheets) HTML ko **style** karta hai — colors, spacing,
fonts, layout, animations. "Cascading" ka matlab hai styles rules ke ek
order mein apply hote hain (specificity + order matters).

## Ways to Add CSS

```html
<!-- External (best practice) -->
<link rel="stylesheet" href="style.css" />

<!-- Internal -->
<style> body { color: red; } </style>

<!-- Inline (avoid, hard to maintain) -->
<p style="color: red;">Text</p>
```

Always prefer **external CSS** — clean separation, reusable, cacheable.

## The Box Model

Har HTML element ek box hai:

```
content → padding → border → margin
```

```css
.box {
  width: 200px;
  padding: 16px;
  border: 1px solid #ccc;
  margin: 20px;
  box-sizing: border-box; /* padding/border width ke andar count hote hain */
}
```

`box-sizing: border-box` almost hamesha use karo — layout math simple ho jata hai.

## Selectors — Quick Reference

| Selector | Matches |
|---|---|
| `.class` | Class wale elements |
| `#id` | Ek specific ID wala element |
| `element` | Sab elements us tag ke |
| `.parent .child` | `.parent` ke andar `.child` |
| `.a, .b` | `.a` ya `.b` dono |
| `:hover`, `:focus` | Interactive states |

## Flexbox (1D Layout)

Row ya column mein elements arrange karne ke liye.

```css
.container {
  display: flex;
  justify-content: space-between; /* horizontal alignment */
  align-items: center;            /* vertical alignment */
  gap: 16px;
}
```

- [ ] `flex-direction: row | column`
- [ ] `justify-content` — main axis alignment
- [ ] `align-items` — cross axis alignment
- [ ] `flex-wrap: wrap` — items next line pe jaayein agar space na ho

## Grid (2D Layout)

Rows aur columns dono control karne ke liye.

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

**Flexbox vs Grid**: Ek row/column ke liye Flexbox, poora page layout ya
card grids ke liye Grid.

## Responsive Design (Media Queries)

```css
@media (max-width: 640px) {
  .grid {
    grid-template-columns: 1fr;
  }
}
```

Mobile-first approach: pehle mobile ke liye style likho, phir `min-width`
media queries se bade screens ke liye adjust karo.

## Useful Units

| Unit | Use |
|---|---|
| `px` | Fixed size |
| `%` | Parent ke relative |
| `rem` | Root font-size ke relative (scalable) |
| `vw` / `vh` | Viewport width/height ka % |

## Common Mistakes

- `box-sizing: border-box` set na karna (padding se layout break hona)
- Bahut zyada `!important` use karna
- Fixed `px` widths hardcode karna instead of responsive units
- Flexbox aur Grid dono ek hi jagah confuse karna

## Practice Ideas

- Card layout (Flexbox se)
- Responsive navbar (mobile mein collapse ho)
- Photo gallery (Grid se)

## Resources

- [MDN CSS Docs](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [CSS-Tricks — Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [CSS-Tricks — Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
