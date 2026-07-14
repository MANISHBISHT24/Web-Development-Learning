# Frontend, Backend & the Server — Notes
**Full-Stack Internship · Module 4 · Backend · Day 13**

---

## 1. Har web app ke do hisse

Har website do parts mein bata hota hai jo aapas mein baat karte hain:

- **Frontend** — jo tum dekhte/click karte ho, **browser** mein chalta hai
- **Backend** — logic aur data, **server** pe kahin aur chalta hai

> **Yaad rakho:** Frontend puchta hai (asks), backend jawab deta hai (answers).

---

## 2. Frontend — jo user dekhta hai

Frontend **user interface** banata hai. Yeh **browser ke andar** chalta hai aur handle karta hai jo user dekhta/karta hai.

### Languages
| Language | Kaam |
|---|---|
| HTML | Structure |
| CSS | Styling |
| JavaScript | Behaviour |

### Frameworks & Libraries
- **Modern "big three":** React, Angular, Vue.js
- **Purane tools (abhi bhi milte hain):** jQuery, Backbone.js

**Frontend karta kya hai:** UI, user interactions, animations, forms, page render karna. Sab **browser mein** chalta hai.

---

## 3. Backend — engine jo peeche kaam karta hai

Backend **server pe** chalta hai, browser mein nahi. User ko yeh **kabhi direct nahi dikhta**. Yeh peeche real kaam karta hai.

### Languages & Frameworks
- **Node.js + Express.js** — JavaScript server pe (jo hum use kar rahe hain)
- Doosre options: Python, Java, PHP, ASP.NET, JSP

### Backend kya karta hai
- **Business logic** run karta hai (app ke rules)
- **Database** se connect hota hai
- **Authentication & authorization** handle karta hai (tum kaun ho, kya kar sakte ho)
- **APIs** banata hai jo frontend call karta hai
- **Data wapas bhejta hai** frontend ko

---

## 4. Application Server

**Application server** woh software hai jo **beech mein** baithta hai — request receive karta hai, backend logic run karta hai, response wapas bhejta hai.

> **Hamare case mein:** Node.js + Express.
> Node ke through JavaScript server pe chalta hai, Express requests handle karne wala framework hai. Dono milke hamara **application server** banate hain — jo client request leta hai aur response deta hai.

---

## 5. Poora Web Flow (ek click se screen update tak)

```
BROWSER (user yahan hai)
     ↓
FRONTEND (HTML + CSS + JS · React/Angular/Vue)
     ↓  HTTP request
APPLICATION SERVER (Node.js + Express)
     ↓
BUSINESS LOGIC (app ke rules yahan chalte hain)
     ↓
DATABASE (data store & fetch hota hai)
     ↑  response (JSON)
FRONTEND UPDATES THE UI (screen change hoti hai)
```

**Round trip ki tarah socho:** Request **neeche** jaati hai (browser → database), phir response (usually JSON) **upar** wapas aati hai, aur frontend naye data ke saath screen redraw karta hai.

---

## 6. Frontend vs Backend — ek nazar mein

| | Frontend | Backend |
|---|---|---|
| **Runs in** | Browser | Server |
| **User dekhta hai?** | Haan, directly | Nahi, hidden |
| **Job** | UI, interaction, display | Logic, data, security |
| **Languages** | HTML, CSS, JS | Node, Python, Java, PHP |
| **Frameworks** | React, Angular, Vue | Express, Django, Spring |
| **Kisse baat karta hai** | User + API | API + database |

---

## 7. Interview ke liye — ek line mein

**Frontend:** Jo users dekhte aur interact karte hain.

**Backend:** Requests process karta hai, business logic run karta hai, aur database handle karta hai.

**Application server:** Software (jaise Node.js + Express) jo HTTP requests receive karta hai, backend logic run karta hai, aur client ko response wapas bhejta hai.

> **Ek saans mein pura concept:**
> Frontend puchta hai → application server process karta hai aur database se baat karta hai → JSON wapas bhejta hai → frontend screen update kar deta hai.

---

## Quick Revision Checklist
- [ ] Frontend = browser, Backend = server — yeh basic split yaad hai
- [ ] Frontend languages: HTML, CSS, JS
- [ ] Backend languages: Node.js/Express (+ alternatives: Python, Java, PHP)
- [ ] Application server ka role samajh mein aata hai (middle mein baithta hai)
- [ ] Poora flow bol sakta hoon: Browser → Frontend → Server → Logic → Database → wapas
- [ ] Frontend vs Backend table yaad hai
- [ ] Teeno one-liners (frontend/backend/application server) bol sakta hoon
