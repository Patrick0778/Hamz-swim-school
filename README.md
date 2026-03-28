# Hamz Swim School

Static website for **Hamz Swim School** — a swimming instruction and pool services brand led by *Coach Magoba Brian (Coach Hamz)*.  
This repo contains the site pages (Home / Shop / Services) plus a simple **admin dashboard** that updates dynamic content stored in **Firebase (Firestore)**.

## What's in this repository

### Pages
- `index.html` — Home page + About section
- `services.html` — Services + lesson availability schedule
- `shop.html` — Swim gear shop page
- `admin.html` — Admin dashboard (login + manage content)

### Assets
- `css/style.css` — Site styling
- `js/main.js` — Main client logic (theme toggle, marquee, poster/ad, calendar, etc.)
- `js/auth.js` — Admin authentication helpers
- `js/database.js` — Firestore read/write helpers
- `imgs/` — Images used across the site

### Firebase / Firestore
- `.firebaserc` — Firebase project mapping (default: `hamz-swim-school`)
- `firebase.json` — Firebase Hosting configuration (serves from project root)
- `firestore.rules` — Firestore security rules (public reads for select collections; authenticated writes)

## Features

- Responsive marketing site (Home / Services / Shop)
- WhatsApp "Chat/Order" links embedded in pages
- Light/Dark theme toggle (UI switch in the navbar)
- Floating marquee shown at the bottom of pages (content stored in Firestore)
- Admin dashboard to manage:
  - Floating marquee text
  - Shop products (Firestore-backed)
  - Home page poster/ad (Firestore-backed)
  - Lesson availability calendar (Firestore-backed)

## Local development

This is a static site (no build step required).

### Option A: Run a local static server
You can open `index.html` directly in a browser, but using a local server is recommended.

Example using Python:

```bash
python -m http.server 8080
```

Then visit:

- http://localhost:8080/index.html

### Option B: Firebase Hosting emulation
If you use Firebase locally:

```bash
npm i -g firebase-tools
firebase login
firebase emulators:start
```

## Deploy (Firebase Hosting)

This repo is set up for Firebase Hosting with:

- `public: "."` (the site root)
- rewrite `** -> /index.html` for SPA-style routing (even though pages are separate HTML files)

Deploy:

```bash
firebase use --add
firebase deploy
```

## Firestore data model (expected)

The site/admin scripts expect these collections:

- `products` — shop items  
- `settings` — global UI settings (e.g., marquee text, poster content)
- `availability` — lesson schedule by date

> Exact document IDs/fields depend on the implementation in `js/database.js` / `js/main.js`.

## Security notes

Firestore rules in `firestore.rules` allow:
- public reads for `products`, `settings`, and `availability`
- create/update/delete only for authenticated users

Before going live, review rules and ensure admin access is properly restricted.

## Credits

- Original upstream project: `kalungim24/Hamz-swim-school`
- This repository: `Patrick0778/Hamz-swim-school` (fork)

## License

No license file is currently included in this repository. If you intend to make this reusable by others, add a `LICENSE` file (e.g., MIT).
