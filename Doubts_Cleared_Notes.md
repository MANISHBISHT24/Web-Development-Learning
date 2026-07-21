# Doubts Cleared - Revision Notes

Full-Stack Internship ke doubt session ka summary — sabse simple words mein, revision ke liye.

---

## 1. MVC Architecture (Himanshu · Day 15)

Restaurant wali analogy yaad rakho:

| Restaurant | Code | Kaam |
|---|---|---|
| Door & signs | Route | Sahi jagah bhejta hai |
| Waiter | Controller | Order leta hai, khana laata hai |
| Kitchen | Model | Data janta hai, taiyaar karta hai |
| Plate on table | View (frontend) | Jo dikhta hai |

**Golden rule:** Waiter kabhi khana nahi banata. Kitchen kabhi table pe nahi aati.
- **Controller** → `req` aur `res` janta hai
- **Model** → sirf `data` janta hai, kabhi `res.json()` nahi bhejta

```js
// routes/documents.js -> door
router.get("/documents", documentsController.getAll);

// controllers/documentsController.js -> waiter
getAll = async (req, res) => {
  const docs = await Document.findAll(); // kitchen se pucho
  res.json(docs); // wapas le aao
};

// models/Document.js -> kitchen
findAll = () => {
  return readFromFile(); // data janta hai, res kabhi touch nahi karta
};
```

⚠️ Agar controller file read kar raha hai → wo kitchen mein ghus gaya.
⚠️ Agar model `res.json()` bhej raha hai → cook table pe aa gaya. Dono galat hai.

---

## 2. Backend & APIs (Mayank, Deepesh, Mohit · Day 14)

Website ke do halves — alag jagah rehte hain, aapas mein baat karte hain (API se).

- **Frontend** = jo dikhta hai (browser mein)
- **Backend** = jo nahi dikhta (server pe)
- **API** = shop counter — tum storeroom mein khud nahi jaate, counter pe maango

### Har conversation ki 4 cheezein

| Word | Matlab |
|---|---|
| Request | Tum kuch maang rahe ho |
| Response | Jo wapas aaya |
| Status code | Kaam hua ya nahi? 200 = haan, 404 = mila nahi, 500 = hum toot gaye |
| JSON | Common language jisme dono baat karte hain |

### Postman kyun zaroori hai?
Browser address bar sirf **GET** kar sakta hai (mangna). Postman se create, update, delete bhi kar sakte ho.

### Poori journey (start to finish)

```
BROWSER (button click)
   ↓ request
ROUTE (kaunsa door?)
   ↓
CONTROLLER (waiter)
   ↓
MODEL (kitchen)
   ↓
DATA (jahan cheezein rakhi hain)
   ↑ JSON ban kar wapas aata hai
SCREEN CHANGE HO JAATI HAI
```

---

## 3. JavaScript, Basic to Advanced (Namrata · Day 9)

Sab kuch bas **cheezein rakhna** aur **unpe kaam karna** hai.

- **Object** = labelled box → `const student = { name: "Rahul", marks: 92 }`
- **Array** = boxes ki line → `const students = [{...}, {...}, {...}]`

### Array methods — kaam samajhne ka trick

Poocho: **"kitni cheezein wapas chahiye?"**

| Method | Bol rahe ho | Wapas milta hai |
|---|---|---|
| `forEach` | "har naam padho" | kuch nahi |
| `map` | "sirf naam ki nayi list do" | nayi row |
| `filter` | "90 se upar wale rakho" | chhoti row |
| `find` | "Aman wala laao" | ek box |
| `some` | "koi pass hua?" | yes/no |
| `every` | "sab pass hue?" | yes/no |
| `sort` | "marks se line up karo" | reordered row |
| `reduce` | "sab marks jodo" | ek number |

- Kai cheezein chahiye → `map`, `filter`
- Ek cheez chahiye → `find`
- Ek number chahiye → `reduce`
- Yes/no chahiye → `some`, `every`
- Kuch nahi chahiye, bas karna hai → `forEach`

---

## 4. Error Handling (Unishka · Backend)

Seatbelt jaisa hai — crash hone ki planning nahi karte, par pehen lete ho taaki crash ho bhi jaye to theek raho.

### Do rules
1. **Server ko kabhi mat marne do** — ek galat request se sab down nahi hona chahiye
2. **Hamesha jawab do** — chahe "no" ho, chup rehna sabse bura response hai

```js
app.get("/api/documents/:id", async (req, res) => {
  try {
    const doc = await Document.findById(req.params.id);
    if (!doc) {
      return res.status(404).json({ error: "Not found" });
    }
    res.json(doc);
  } catch (err) {
    console.error(err);
    res.status(500).json({ error: "Something went wrong" });
  }
});
```

### Status codes — kiski galti?

| Code | Matlab | Kiski galti |
|---|---|---|
| 200 | "yeh lo" | kisi ki nahi, ho gaya |
| 201 | "bana diya, yeh lo" | kisi ki nahi |
| 400 | "tumne rubbish bheja" | unki |
| 401 | "tum kaun ho pata nahi" | unki |
| 404 | "yeh cheez hai hi nahi" | unki |
| 500 | "main toot gaya, sorry" | hamari |

⚠️ **Sabse badi galti:** 200 OK bhejna jisme error message ho. Ye khaali plate deke bolne jaisa hai "enjoy your meal". 404 ya 500 hi bolo, honest raho.

---

## 5. Backend Revision (Yatin)

**Backend kya hai?** Ek program jo baithke wait karta hai. Koi kuch poochta hai, wo jawab dhoondta hai, reply karta hai. Phir wapas wait karta hai. Bas yahi hai.

### Folders

| Folder | Kya hai | Restaurant |
|---|---|---|
| `routes/` | kaunsa URL kahan jaata hai | door aur signs |
| `controllers/` | req leta hai, res bhejta hai | waiter |
| `models/` | data janta hai | kitchen |
| `middleware/` | route se pehle chalta hai | security guard |

### Middleware — door ka guard

Route se pehle chalta hai. Check karta hai, note karta hai, ya rok deta hai. Phir `next()` bolta hai — "theek hai, jaane do".

```js
app.use(express.json());   // JSON unpack karo — SABSE PEHLE
app.use(logger);            // kaun aaya likho
app.use("/api", routes);    // asli door
```

⚠️ **Order sab kuch hai.** Agar `express.json()` routes ke neeche hai, to guard door ke peeche khada hai. Parcel kabhi khulta nahi, `req.body` undefined rehta hai. Iss galti mein log ghanta barbaad karte hain.

### Interview ke liye ek line
> "Request aati hai, route usse controller ko bhejta hai, controller model se data maangta hai, model return karta hai, controller JSON aur status code ke saath wapas bhejta hai."

### Yaad rakhne wale 5 words
- **req** — unhone kya bheja
- **res** — tum kaise jawab doge
- **route** — kaunsa door
- **controller** — kaun handle karta hai
- **model** — data kaun janta hai

---

## 6. Git & GitHub (Jiya Noor)

Video game ki save point jaisa: **Git** = laptop pe save karna. **GitHub** = internet pe upload karke dosto ko dikhana.

### 3 confusing steps

| Command | Kya karta hai | Jaisa |
|---|---|---|
| `git add .` | files select karta hai | saaman box mein rakhna |
| `git commit -m "..."` | note ke saath save karta hai | box tape karke label lagana |
| `git push` | GitHub pe bhejta hai | box post karna |

⚠️ **Sabse badi galti:** commit karke laptop band kar dena aur sochna ki GitHub pe aa gaya. Nahi aaya — jab tak push nahi karoge.

### Poora flow

```bash
# naya project shuru karte waqt, sirf ek baar
git init
git remote add origin https://github.com/you/your-repo.git

# har baar kaam karne ke baad
git add .
git commit -m "added css styling and the 3 projects"
git push origin main
```

Baar baar karo — hafte ke end mein ek baar nahi. Chhota sa kaam khatam hua, commit karo.

### Do aur daily use wale

- `git status` → "main kahan hoon? kya badla?"
- `git clone <url>` → "us project ki copy de do"

### Achhe commit messages likho

| Bura | Achha |
|---|---|
| update | added hover states to buttons |
| asdf | fixed navbar breaking on mobile |
| final final v2 | added css.md learnings |

GitHub tumhara asli CV hai — PDF nahi. Log tumhara kaam karne ka tareeka dekhte hain.

---

## 7. Same-origin vs Cross-origin (CORS)

Jab frontend backend ko call karta hai aur browser CORS ka shor machata hai — ye samjho:

### Origin kya hai?
Teen cheezein: **protocol + domain + port**. Sab match → same origin. Ek bhi alag → cross-origin.

```
https://shop.com/products   // https | shop.com | 443
https://shop.com/cart       // SAME origin
http://shop.com             // protocol alag -> CROSS
https://api.shop.com        // domain alag -> CROSS
https://shop.com:3000       // port alag -> CROSS
```

Apartment building jaisa: same origin = apne flat ke andar ghoomna. Cross-origin = doosre flat ka darwaaza khatkhataana.

### Browser kyun rokta hai?
User ko protect karne ke liye. Warna koi bhi evil website chupke se tumhari bank site ko call kar sakti thi tumhare logged-in session se.

⚠️ **Confusion wali baat:** Block **browser** karta hai, tumhara server nahi. Server ne theek se jawab diya — browser ne rok diya kyunki allowed mark nahi tha. Isliye Postman mein kaam karta hai, browser mein nahi.

### Fix: CORS

```js
const cors = require("cors");
app.use(cors()); // koi bhi origin allow (seekhne ke liye theek hai)

// ya sirf apna frontend allow karo (real apps ke liye better)
app.use(cors({ origin: "https://myapp.com" }));
```

### Quick reference

| Term | Ek line mein |
|---|---|
| Origin | protocol + domain + port, teeno |
| Same-origin | teeno match, hamesha allowed |
| Cross-origin | ek alag, default blocked |
| CORS | server ka tareeka bolne ka "main allow karta hoon" |

---

*Doubt aaye to phir se pucho — group mein, 5pm ko, ya seedha instructor se. Poochne se koi bewakoof nahi lagta.*
