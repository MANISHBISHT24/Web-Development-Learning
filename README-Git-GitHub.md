# Git & GitHub Learning Notes

Core concepts of version control — tracking changes and collaborating on code.

## Git vs GitHub

- **Git** — version control tool jo aapke computer pe local chalta hai
  (code ki history track karta hai)
- **GitHub** — Git repos ko online host karne, share karne, aur
  collaborate karne ki website

## First-Time Setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## Starting a Repo

```bash
git init                  # naye project ko Git repo banao
git clone <url>            # existing GitHub repo ko download karo
```

## The Basic Workflow

```bash
git status                 # kya changed hai, dekho
git add file.js             # ek specific file ko staging mein daalo
git add .                   # sab changed files staging mein daalo
git commit -m "message"     # staged changes ko save karo, ek snapshot
git push                    # commits ko GitHub pe bhejo
git pull                    # GitHub se latest changes lao
```

**Mental model**: `add` = "isko commit ke liye ready karo", `commit` =
"is state ka snapshot save karo", `push` = "GitHub pe upload karo".

## Branches

```bash
git branch                       # existing branches dekho
git branch feature-login          # nayi branch banao
git checkout feature-login        # us branch pe switch karo
git checkout -b feature-login     # banao + switch, ek saath
git branch -M main                # current branch ka naam "main" karo
```

**Kyun use karo**: Har naya feature/fix apni branch pe karo — `main`
branch hamesha stable/working rahe.

## Connecting to GitHub

```bash
git remote add origin https://github.com/username/repo-name.git
git push -u origin main
```

`-u` ek baar set karne ke baad, aage sirf `git push` likhne se kaam chal jayega.

## Pull Requests (PRs)

1. Apni branch pe changes push karo
2. GitHub par jaake **"Compare & pull request"** click karo
3. Description likho ki kya change kiya
4. Team review karke **merge** karta hai `main` mein

## Common Commands Cheat Sheet

| Command | Kya karta hai |
|---|---|
| `git log` | Commit history dekho |
| `git diff` | Changes dekho jo abhi commit nahi hue |
| `git stash` | Changes temporarily side pe rakho |
| `git reset` | Staged changes wapas le lo |
| `git revert` | Ek purane commit ko safely undo karo |

## .gitignore

Files/folders jo Git track na kare (jaise `node_modules`, `.env`):

```
node_modules/
.env
dist/
.DS_Store
```

## Common Mistakes

- `.env` ya passwords accidentally commit kar dena (secrets kabhi push mat karo)
- Directly `main` branch pe kaam karna (team projects mein risky hai)
- Bina message ke commit karna (`git commit -m ""` — hamesha meaningful message likho)
- `git push` se pehle `git pull` na karna (conflicts se bacha jaata hai)

## GitHub Pages (Free Static Hosting)

1. Repo → **Settings → Pages**
2. Source: **Deploy from a branch**, Branch: **main**, Folder: **/ (root)**
3. Live URL milega: `https://username.github.io/repo-name/`

## Practice Ideas

- Apna pehla repo banao aur push karo
- Ek branch banao, change karo, PR banao (khud ke against bhi)
- Kisi open-source repo ko fork karke ek chhota fix try karo

## Resources

- [Git Official Docs](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com/)
- [Learn Git Branching (interactive)](https://learngitbranching.js.org/)
